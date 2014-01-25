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

3. Production and staging environent
-----------
- Access to remote servers SHOULD be secured by public key
- Debugging extensions MUST NOT be used in production environment
- All used PHP extenstions SHOULD be in stable version. If unstable version is used it MUST be properly testen prior to deployment
- When setting up remote server directory listing MUST be disabled
- Project backend MUST NOT be accessible from the Internet. It's RECOMMENDED to place it in home dir and create symlink to /var/www

4. Basic coding standards
-----------
- Code MUST follow all rules outlined in [PSR-0][]
- Code MUST follow all rules outlined in [PSR-1][]
- Code MUST follow all rules outlined in [PSR-2][]
- Code MUST follow all rules outlined in [PSR-3][]
