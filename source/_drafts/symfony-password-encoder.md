n of Symfony2 Password encoders

A very simple breakdown of how the password encoding works with Symfony 2.

## Encoder factory

The encoder factory is where you get your password encoders from. You pass in a User entity and it returns an Encoder. Encoders are created from encoder configs and stored within the factory, that is there is only a single instance of the encoder unless you clone it outside of the factory. The encoder configs are passed to the factory upon creation. Once a factory is created there is no way of adding new encoders as there is no add method and the internal class variable holding these is private. The encoder config array is generated from the encoders assigned to a user entity. If the encoder is not used by anything then Symfony just doesn't load it.

When fetching an encoder you can either pass in a User entity or you can pass in the string of the class you want to find the encoder for. This behaviour can be leaveraged so you define encoders with ids that aren't class named and then just pass in the name of the encoder you want.

```yml
bcrypt:
  algorithm: bcrypt
```

```php
$encoder = $encoderFactory->getEncoder('bcrypt');
```

## Creating your own Password Encoder

To create your own password encoder you have to create your own encoder class implementing `Symfony\Component\Security\Core\Encoder\PasswordEncoderInterface` interface. You can extend the `Symfony\Component\Security\Core\Encoder\BasePasswordEncoder` class which has several helper functions which you may want to use in your own Encoder.

Here's an example Encoder class.

```php
<?php

namespace Icambridge\Encoder;

use Symfony\Component\Security\Core\Exception\BadCredentialsException;
use Symfony\Component\Security\Core\Encoder\BasePasswordEncoder

/**
 * A super duper silly password encoder, no one should ever use!
 */
class SuperDuperSillyEncoder extends BasePasswordEncoder
{  
    private $ignorePasswordCase;

    public function encodePassword($raw, $salt)
    {
        if ($this->isPasswordTooLong($raw)) {
            throw new BadCredentialsException('Invalid password.');
        }

        $rawMd5 = md5($raw);
        $saltSha = sha1($salt);

        $encodableString = $this->mergePasswordAndSalt($rawmd5, $saltSha);
        $encodedString = $encodableString . $encodableString[0] . $encodableString[1];

        return $encodedString;
    }

    public function isPasswordValid($encoded, $raw, $salt)
    {
        if ($this->isPasswordTooLong($raw)) {
            return false;
        }

        $pass2 = $this->encodePassword($raw, $salt);

        if (!$this->ignorePasswordCase) {
            return $this->comparePasswords($encoded, $pass2);
        }

        return $this->comparePasswords(strtolower($encoded), strtolower($pass2));
    }
}
```

Once you have created the class you have to define it in your services container configuration.

```xml
<service id="encoder.super_duper_silly" class="Icambridge\Encoder\SuperDuperSillyEncoder" />
```

Then to have it loaded into the Encoder factory you need to assign it to a user entity in your security.yml file like so.

```yml
Icambridge\Entity\User:
    id: encoder.super_duper_silly
```

## Password encoder based on the User entity

The EncoderAwareInterface allows you to return the key for the encoder you want for that user.

```php
<?php

namespace Icambridge\Encoder;

class User implements EncoderAwareInterface
{
  public function getEncoderName()
  {
    return "bcrypt";
  }
}
```

The key for the encoder is key that was put into your security.yml config. In the below example we have bcrypt available as a key as well as "Icambridge\Entity\InsecureUser".

```yml
Icambridge\Entity\InsecureUser:
  algorithm: plaintext
bcrypt:
  algorithm: bcrypt
```
