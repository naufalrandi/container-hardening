# Run a Docker Container with the Seccomp Profile
Use the --security-opt option to specify the custom seccomp profile when running a Docker container:

`docker run --security-opt seccomp=custom-seccomp.json ubuntu:latest`

# Test the Seccomp Profile
To verify that the seccomp profile is working as expected, you can try running commands inside the container that are allowed and disallowed by the profile.

## Allowed system calls:

`docker run --security-opt seccomp=custom-seccomp.json ubuntu:latest /bin/bash -c "echo 'This should work'"`

This command should succeed because write is allowed.

## Disallowed system calls:

`docker run --security-opt seccomp=custom-seccomp.json ubuntu:latest /bin/bash -c "exec /bin/ls"`

This command should fail because execve is blocked. You should see an error indicating that the execve system call is not permitted.