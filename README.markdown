# Simple Rotate Children Password Generator

This is a rather simple idea to set a new password for a (child/guest) user each day using what is available already.
The password should deterministic and not be easy to guess.
We assume the computer is not running thoughout the night and the password can be set on boot time for each new day.

## rl;dr
The password generated as a product of the date with a modulo, its mirror and the mirrored modulo plus a fixed addend.
This way it is deterministic, not guessable and never 0. We adjust the length by cutting to first digits, no longer than the addend.
To create longer numbers the modulo and the addend can be adjusted, the date format string would be another option.

## Usage
To enable easy lookup on the web there is [JavaScript version](simplercpasswd.html).
<!-- To get the password on the shell there is a [Shell version](simplercpasswd.sh). -->
For that we use [rc.local](rc.local) so it's compatible with systemd (rc-local service).[^1]
The file `rc.local` needs to be made executeable for superuser and located in the `/etc/` directory after setting the correct username.

## Alternative Solutions
A better solution might be TOTP; here we chose not to implement HMAC and hashing or depend on more tools.
There are already implementations for e. g. two factor authentication (2FA).

## Todo
Alternatively the number could be converted to words from a dictionary. This might be added later.
Maybe add more comfort for the js/shell generators to lookup for certain days.
There could be more checks and error reporting.

## Out of Scope
With systemd timer or cron it would even be possible to reset the password when the day changes, warn and logout the user eventually.
Another ppssibilty might be to have time restrictions for certain users.

[^1]: https://www.cyberciti.biz/faq/how-to-enable-rc-local-shell-script-on-systemd-while-booting-linux-system/
