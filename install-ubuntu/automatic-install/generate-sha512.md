# Generate SHA-512 for Password

"openssl passwd -6" at the linux command line will do this SHA-512 hash for you!

```shell
printf '${PASSWORD}' | openssl passwd -6 -salt '${SALT_KEY}' -stdin

```

## Reference

- [how to generate crypted password for auto install](https://askubuntu.com/questions/1261451/how-to-generate-crypted-password-for-auto-install)
- [Why is the output of "openssl passwd" different each time?](https://unix.stackexchange.com/questions/510990/why-is-the-output-of-openssl-passwd-different-each-time)
- [How do I set a custom password with Cloud-init on Ubuntu 20.04?](https://stackoverflow.com/questions/61591885/how-do-i-set-a-custom-password-with-cloud-init-on-ubuntu-20-04)
