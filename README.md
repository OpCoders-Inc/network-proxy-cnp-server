# CNP Server
Commodore Network Protocol Server

This is the Commodore Network Protocol server, which is used to allow the C64 OS network stack to bridge to the internet.

Version 1.5 adds several important features.

- Ability to pause and resume sockets (in use by C64 OS v1.08)
- CNP event logging (events can be viewed from account at c64os.com)
- Added packet acknowledgement timeouts, for packet resending.
- This version switches from using "require" to using "import" for node modules.
