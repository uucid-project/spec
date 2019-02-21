# UUCID v1 Spec

A UUCID is simply a UUID v4 id formatted in a way that ensures natural chronological sort. This is extremely helpful in databases where records can be
spread across multiple servers.

-> [View the list of current implementations](https://github.com/uucid-project/spec/blob/master/Implementations.md)

## Example

10155077-7700-4688-b1cf-cca495323496

## Each UUCID v1 is comprised of two parts:

1. Millisecond UNIX timestamp.

   - Minimum timestamp is `-8640000000000` (`1696-03-17T00:00:00.000Z`).
   - Maximum timestamp is `99999999999999` (`5138-11-16T09:46:39.999Z`).
   - All timestamp values are automatically converted to a string and
     left-padded with `0` to ensure it's exactly 14 characters.

2. 15 character random string using only lowercase a-z and 0-9.
   Cryptographically-secure generation methods are recommended.

## The parts are then combined using the following order:

1. The first character must be a 0 or a 1:

   - 0 if the provided millisecond timestamp is **before** the UNIX Epoch (January 1st, 1970).
   - 1 for all other dates.

2. `timestampStr.substring(0, 7)`.

3. Hyphen ("-") separator.

4. `timestampStr.substring(7, 11)`.

5. Hyphen ("-") separator.

6. `4` to denote that it's a UUIDv4 format UUID.

7. `timestampStr.substring(11, 14)`.

8. Hyphen ("-") separator.

9. One of the following numbers or **lowercase** characters chosen at random: (required for UUID v4 spec):

   - "8", "9", "a", or "b"

10. `randomStr.substring(0, 3)`

11. Hyphen ("-") separator.

12. `randomStr.substring(3, 15)`

---

## Sponsors

- [Loomble](https://loomble.com/)

## Maintainers

- [Jay Rylan](https://jayrylan.com/)

## License

[OWFa-1.0](https://github.com/uucid-project/spec/blob/master/LICENSE)
