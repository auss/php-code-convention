[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[PSR-3]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[XDebug]: http://xdebug.org
[XHProf]: https://github.com/facebook/xhprof

Overwiev
===================
This document describes the mandatory requirements and recommendations for coding in PHP and creating PHP environments.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

1. Recommended PHP version
-----------
Recommended PHP version is 5.5.x. Developer SHALL NOT use version lower than 5.4. All versions MUST be up to date.

2. Development environment
-----------
- Developer MUST use PHP with Apache2. 
- It's RECOMMENDED to use *nix OS (Linux, MacOS X)
- Developer SHOULD use debugging extensions ([XDebug][], [XHProf][])

3. Production and staging environment
-----------
- Access to remote servers SHOULD be available only by Public Key Infrastructure
- Debugging extensions MUST NOT be used in production environment
- All used PHP extenstions SHOULD be in stable version. If unstable version is used it MUST be properly tested prior to deployment
- When setting up remote server, directory listing MUST be disabled
- Project backend MUST NOT be accessible from the Internet. It's RECOMMENDED to place it in home dir and create symlink to /var/www

4. Basic coding standards
-----------
- Code MUST follow all rules outlined in [PSR-0][]
- Code MUST follow all rules outlined in [PSR-1][]
- Code MUST follow all rules outlined in [PSR-2][]
- Code MUST follow all rules outlined in [PSR-3][]

5. Naming conventions
-----------
Every developer SHOULD be able to read code like a book. Proper naming is much better than hundrets of documentation lines.


### 5.1. Variables
- Variable name MUST describe its purpose. 
- All variables MUST be declared in ```camelCase```

Example:
```php
<?php

// bad
$m = new Movie();
$mc = new MovieCollection();

// good
$movie = new Movie()
$movieCollection = new MovieCollection();
```
### 5.2. Functions
- Function visibility MUST be declared (public, protected, private). 
- Function declaration MUST follow given pattern: ```public [static] function functionName() ```
- Functions MUST be sorted by visibility:
    - public
    - protected
    - private
- Function name MUST describe its purpose using verbs like is, has, can, get, set. Example:
```php
<?php

//bad
class BadMovie
{
    protected $rate = 0;
    
    public function rated()
    {
        return $this->rate > 0;
    }
    
    
    public function rate()
    {
        return $this->rate;
    }
}


//good
class GoodMovie
{
    protected $rate = 0;
    
    public function hasRate()
    {
        return $this->rate > 0;
    }
    
    
    public function getRate()
    {
        return $this->rate;
    }
}
```

### 5.3. Classes
- Class name MUST describe its purpose. 
Example:
```php
<?php
// bad
class Movies
{
}

// good
class MovieCollection
{
}
```
- Class name MAY NOT be unique in whole project scope. It's handled by namespaces.
Example:
```php
<?php
namespace \BM\Api1;
class Response
{
}

namespace \BM\Api2;
class Response
{
}
```

- Special types of classes MUST be followed by suffixes:
    - *Trait for Traits: ```trait SomeTrait ```
    - *Collection for collections: ```class SomeCollection ```
    - *Controller for controllers: ```class SomeController ```
- Class MUST be used only for the purpose it was designed for. For example: Developer CAN NOT use MoviesCollection to store collection of Cookies.


6. Exceptions
----------
- Custom exception constructor MUST accept exception message
- Custom exception MAY have default message. 
- When message is passed as parameter in constructor it MUST override default message
- Custom exceptions SHOULD extend one of two base types:
    - InternalException - content of this exception MUST NOT be displayed (except for dev environment)
    - FriendlyException - content of this exception MAY be displayed
- All exceptions SHOULD be handled
- InternalException MUST be reported by email
- FriendlyException MAY be reported by email
- Different types of exceptions SHOULD be catched in multiple catch blocks
- There SHOULD be catch block for default Exception
- All exceptions MUST be attached to variable $e
```php
<?php
try {

} catch (FirstException $e) {

} catch (SeconException $e) {

} catch (Exception $e) {

}
```


7. Typehinting
---------
- It's RECOMMENDED to hint the type of variable passed as function argument.
- When variable is returned from another function it's type SHOULD be validated. 

Example:
```php
<?php

// bad
class BadMovie
{
    protected $director;
    
    public function setDirector($director)
    {
        $this->director = $director;
    }
    
    
    public function getDirector()
    {
        return $this->director;
    }
}

$badMovie = new BadMovie();
$director = $badMovie->getDirector();
$director->getName();

// good
class GoodMovie
{
    protected $director;
    
    public function setDirector(Director $director)
    {
        $this->director = $director;
    }
    
    
    public function getDirector()
    {
        return $this->director;
    }
}

$movie = new Movie();
$director = $movie->getDirector();

// bad 
if( $director ) {
    $director->getName();
}

// good
if( $director instanceof Director ) {
    $director->getName();
}
```

8. Return statements
--------
- Return statement SHOULD be preceded by new line unless return is the only statement in function

9. Collections
--------
- Collection name MUST be followed by suffix Collection ```class SomeCollection```
- Collection MUST be iterable
- It's RECOMMENDED to extend ArrayObject
 
