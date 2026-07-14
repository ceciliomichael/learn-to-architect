# Exercise: Networking and Platform Boundaries

## Steps

1. Move network_start and network_stop declarations to network.h.
2. Put the POSIX implementation in network_posix.c.
3. Keep operating-system headers out of main.c.
4. Compile exactly one platform implementation.
5. Document the close and error differences a full socket wrapper must also hide.

## Success check

Application code uses one interface, the build selects one implementation, and platform headers stay inside the platform layer.

