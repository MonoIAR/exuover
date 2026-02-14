# Extended and User-Oriented Versioning 1.0.0

## Abstract
Version format: Major.Minor.Patch.Tweak, with the following increment rules:

1. Major: when you make backward-incompatible or extremely significant changes,
2. Minor: when you add new functionality,
3. Patch: when you fix issues,
4. Tweak: when you make small adjustments that don’t warrant a new Patch number (optional).
If necessary, additional information can be appended after “Major.Minor.Patch.Tweak” as an extension.

## Introduction
In the world of software distribution, we are facing chaos known as “version number hell.”

Traditional [Semantic Versioning](https://semver.org/) (SemVer) is designed for developers and focuses on API compatibility. However, in general applications, video games, content mods (or other primarily user-facing software), there may be no such thing as a “public API,” and thus no concept of API compatibility.

Moreover, if you update the Patch number just because you fixed a typo, it's not worth it; but if you don’t update the version number, users may encounter conflicts after downloading files with the same name but different contents.

In these fields, developers often fall into confusion: some skip version numbers based on mood, while others pile multiple updates into the same version, leaving users unable to judge the risk and value of updates.

As one solution to this problem, I propose extending and modifying the Semantic Versioning standard by shifting the focus of version numbers to a promise of user experience. I call this standard “**Extended and User-Oriented Versioning**.”

## Extended and User-Oriented Version Specification (ExuoVer)
The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, OPTIONAL in this document are to be interpreted as described in RFC 2119.

1. Standard version numbers MUST use the format `X.Y.Z.A`, where X, Y, Z, and A are all non-negative integers and MUST NOT contain leading zeros. X is the Major version, Y is the Minor version, Z is the Patch version, and A is the Tweak version. Each element MUST increase numerically. For example: `1.4.1.1` -> `1.4.1.2` -> `1.4.2`.

2. Once a version is released, you MUST NOT change **any** content of that version. Any modification MUST be released as a new version.

3. Software with a Major version of 0 is in the initial development stage; everything may change at any time, and such software SHOULD NOT be considered “complete” or “stable.”

4. Version 1.0.0.0 SHOULD define the first official release, indicating that the software’s core functionality is complete or stable and ready for large-scale distribution.

5. The Patch version Z (x.y.Z) MUST be incremented when fixing bugs, adjusting values, or making significant performance optimizations. When the Minor version changes, the Patch version MUST reset to zero.

6. The Minor version Y (x.Y.z) MUST be incremented when adding user-visible new features, mechanics, or content, or when making significant modifications to existing content. When the Major version changes, the Minor version MUST reset to zero.

7. The Major version X (X.y.z) MUST be incremented when the software undergoes the following changes:
   - Changes that cause complete data incompatibility,
   - A complete overhaul of UI layout or interaction logic,
   - A change of the underlying engine,
   - A change in the software’s core positioning,
   - A full remake of the software.

8. The Tweak version A (x.y.z.A) SHOULD be incremented for changes that do not warrant increasing the Patch version, such as fixing typos and grammatical errors, minor visual asset adjustments, or modifying content typically invisible to users. When the Major, Minor, or Patch version changes, the Tweak version MUST reset to zero. If the Tweak version is 0, it MAY be omitted. Updates that increment the Tweak version MUST NOT include any compatibility issues.

9. If necessary, you MAY use a suffix at the end of the standard version number to briefly describe the purpose of the version or its development stage, such as “-rebuild,” “-alpha,” “-beta,” etc. The suffix MUST contain only lowercase letters (a–z) and numbers, preceded by a hyphen. They should look like: `2.0.0-unity6`.

10. Version precedence follows left-to-right priority: `1.0.0.0` < `1.0.1.0` < `1.1.0.0` < `2.0.0.0`

11. Version numbers MUST be unique. You MUST NOT release updates by only modifying the suffix. Each version number MUST have only one suffix. If anything needs to be changed, modify the version number.

## About
The ExuoVer specification was created by [MIAR](https://github.com/MonoIAR).
If you have any suggestions, feel free to [submit them on GitHub](https://github.com/MonoIAR/exuover).

## License
[Creative Commons Attribution–ShareAlike 4.0](https://creativecommons.org/licenses/by-sa/4.0/)