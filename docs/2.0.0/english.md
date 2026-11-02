# Extended and User-Oriented Versioning (ExuoVer) 2.0.0

| Item | Content |
| --- | --- |
| Specification | Extended and User-Oriented Versioning |
| Short name | ExuoVer |
| Document version | 2.0.0 (core 2.0.0.0; the tweak is 0 and is omitted per 3.3) |
| Status | Published |
| Date | 2026-11-03 |
| Editor | MIAR STAFF |
| Normative language | Simplified Chinese |
| Supersedes | ExuoVer 1.0.0, see [the 1.0.0 English text](../1.0.0/english.md) |
| License | [Creative Commons Attribution-ShareAlike 4.0](../../LICENSE) |
| Repository | https://github.com/MonoIAR/exuover |

**Cite this document:** MIAR STAFF. *Extended and User-Oriented Versioning (ExuoVer) 2.0.0*. 2026-11-03. https://github.com/MonoIAR/exuover

> This English text is informative. The normative text is the Simplified Chinese version at [ExuoVer.md](../../ExuoVer.md). If the two differ, the Chinese text prevails.

---

## 0. Status of This Document

*[Normative]*

### 0.1 Normative and Informative Sections

Every section of this document is marked normative or informative. Normative sections contain conformance requirements; informative sections provide background, rationale and examples and contain no requirements. Appendices A, C and D are informative; Appendix B is normative.

Informative sections may use normative key words when restating normative content or quoting conditions of the licence; such wording takes its force from the original source.

### 0.2 Key Words

The normative key words in this document are to be interpreted as described in BCP 14 ([RFC 2119], [RFC 8174]). RFC 8174 stipulates that these words carry normative force only when written in all capitals, but Chinese has no letter case, so that rule cannot be applied directly. This document therefore fixes a correspondence between each English key word and a Chinese expression, and that correspondence is normative for the Chinese text:

| English key word | Chinese expression | Meaning |
| --- | --- | --- |
| MUST, REQUIRED, SHALL | 必须 | Absolute requirement; deviation is not permitted |
| MUST NOT, SHALL NOT | 不得 | Absolute prohibition |
| SHOULD, RECOMMENDED | 应当 | Deviation is permitted, but only with a sound reason and after accepting every consequence |
| SHOULD NOT, NOT RECOMMENDED | 不应当 | As above, in the opposite direction |
| MAY, OPTIONAL | 可以 | Genuinely optional; neither adopting nor declining is a defect |

Where the Chinese text uses 必须, 不得, 应当, 不应当 or 可以, the meaning in the table above applies. The strength of a key word does not change with its position, modifiers or tone; a sentence that contains one still carries its own conditions, scope and exceptions.

Every statement in a normative section is normative; the five key words mark the strength of a requirement, not a precondition for being normative. Statements phrased with 应该, 建议, 需要, 推荐 and the like do not constitute requirements.

### 0.3 Normative References

- **[RFC 2119]** Bradner, S. *Key words for use in RFCs to Indicate Requirement Levels*. BCP 14, 1997.
- **[RFC 8174]** Leiba, B. *Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words*. BCP 14, 2017.
- **[RFC 5234]** Crocker, D., Overell, P. *Augmented BNF for Syntax Specifications: ABNF*. 2008.

### 0.4 Informative References

- **[SemVer]** Preston-Werner, T. *Semantic Versioning 2.0.0*. https://semver.org
- **[CC-BY-SA-4.0]** Creative Commons. *Attribution-ShareAlike 4.0 International*. https://creativecommons.org/licenses/by-sa/4.0/

---

## 1. Introduction

*[Informative]*

A version number has to answer one question: what does this update mean for me? When a user sees a new release, they want to know three things — whether they have to relearn how to use the software, whether their existing saves and settings still work, and whether there is anything new to play with or to use.

Semantic Versioning (SemVer) answers a different question: will this update break the code that calls my interface? That answer matters enormously for libraries and frameworks, and often makes no sense for applications, video games and content mods — such software may expose no public programming interface at all, and then interface compatibility is not a thing.

Adopting SemVer directly runs into two concrete problems. First, fixing a single typo would still require a new release; otherwise two files with different contents and the same name would confuse users and distribution channels. Spending a patch number on a typo, however, inflates the version number. Second, test builds are frequent during development, and if every one of them increments the version number, the number stops reflecting anything meaningful.

ExuoVer answers with two moves. First, it moves the meaning of a version number from interface compatibility to the user's cost of migration: each segment states what the user has to do after updating. Second, it introduces a build label that occupies no version number, so a batch of artifacts can be described without inventing a version for it.

## 2. Terminology

*[Normative]*

**Version**: the set of user-facing promises identified by a core. Where this document says "version number", it means the core.

**Version Core**: a decimal sequence of the form `X.Y.Z` or `X.Y.Z.A`, being, in order, the major, minor, patch and tweak numbers.

**Major**, **Minor**, **Patch**, **Tweak**: the first through fourth positions of the core, written X, Y, Z and A.

**Build label (info)**: an annotation of 1 to 64 lowercase letters or digits following a hyphen, see Section 5.

**Version String**: the complete string formed by a core and an optional build label, that is, everything the user sees.

**Canonical Form**: the single normative spelling of a version string, see 3.3.

**Official Release**: within one product line, the first and only occasion on which a given core is offered to users as stable content, carrying no build label, see 5.4 and 7.3.

**Build**: the set of artifacts corresponding to one version string, possibly carrying a build label.

**Artifact**: a file or piece of content distributed to users, such as an executable, a resource pack, an installer or a manifest.

**User-perceivable**: a change in behaviour, content, appearance or performance that a user may notice in normal use. A change discoverable only through logs, debugging tools or inspection of files is not user-perceivable.

**Product Line**: a set of releases whose user-perceivable content is the same. Version numbers of different product lines are not compared with each other and are numbered independently.

**Segment**: one of the four positions of the core, ordered X, Y, Z, A from highest to lowest. "The higher segment" means the one earlier in that order.

**Stable Content**: user-perceivable content that the maintainer has already offered as an official release and promises not to change in a breaking way.

**User-perceivable Content**: the body of wording, levels, values, mechanics and regional content a user encounters while using the software. Appearance adaptation, platform adaptation, input methods and performance are not user-perceivable content.

**Existing Content**: content provided by existing official releases, including official content distributed with the software and third-party extensions the software explicitly supports, such as mods.

**Publish**: to make a set of artifacts available to users. What is published is one version string, see 7.1.

**Compatible**: the user can obtain the same functionality before and after updating without altering data, configuration or established habits of use.

**Precedence**: the ordering of two version strings, determined solely by the core, see Section 6.

**Adopter**: a person or organisation that releases software under this specification.

## 3. Version Format

*[Normative]*

### 3.1 Structure

A version string consists of a core and an optional build label:

```
X . Y . Z [ . A ] [ - info ]
```

X, Y, Z and A are non-negative integers; info is the build label. The tweak A may be omitted, in which case its value is 0.

### 3.2 Grammar

The grammar is given in ABNF per [RFC 5234]:

```abnf
version-string = version-core [ "-" info ]
version-core   = numeric "." numeric "." numeric [ "." numeric ]
numeric        = "0" / ( %x31-39 *DIGIT )
info           = 1*64( DIGIT / %x61-7A )
```

Notes:

- `numeric` is a non-negative integer without a leading zero; a lone `0` is valid.
- `numeric` MUST lie between `0` and `2^63−1`; values outside that range are invalid.
- `info` is 1 to 64 characters drawn from `a` to `z` and `0` to `9`. It is case-sensitive and accepts lowercase only.
- `info` may not be empty; `1.2.3-` is invalid.

### 3.3 Canonical Form

The canonical form of a version string is determined as follows:

1. If the tweak is 0, omit that segment.
2. If the tweak is not 0, write that segment.
3. Keep the build label as it is.

Thus `1.4.2` and `1.4.2.0` denote the same version and the former is canonical; in `1.4.1.1` the tweak is not 0 and therefore MUST be written.

| Requirement | Strength |
| --- | --- |
| User-facing artifacts (file names, release manifests, package metadata, release-note headings, download links) MUST use the canonical form | MUST |
| Parsers MUST accept the canonical form | MUST |
| Parsers MUST accept non-canonical spellings such as `1.4.2.0` and MUST treat them as the same version as `1.4.2` | MUST |
| Comparison, duplicate detection and sorting MUST normalize first; raw strings MUST NOT be compared directly | MUST |

Whitespace surrounding a version string is not part of it. A parser MUST strip leading and trailing whitespace before judging, and MUST NOT let it change the validity of a spelling.

### 3.4 Invalid Forms

The following are invalid and parsers MUST reject them:

| Spelling | Reason |
| --- | --- |
| `01.2.3`, `1.02.3`, `1.2.3.00` | Numbers carry leading zeros |
| `1.2`, `1.2.3.4.5` | Segment count is not 3 or 4 |
| `1..3` | Empty segment |
| `-1.2.3`, `1.2.-3` | Number is not a non-negative integer |
| `1.2.3-` | Empty build label |
| `1.2.3-Alpha` | Build label contains uppercase |
| `1.2.3-alpha-1` | Build label contains a hyphen |
| `1.2.3-alpha.1` | Build label contains a dot |
| `1.2.3+build` | This specification has no build metadata |
| `1.2.3-alpha_beta` | Build label contains an underscore |
| `9223372036854775808.0.0` | Number exceeds the semantic limit in 3.2 (the grammar itself permits any number of digits) |

## 4. Increment Rules

*[Normative]*

### 4.1 The Promise Model

Each segment makes a promise about what the user has to do:

| Segment | Promise |
| --- | --- |
| Major X | You MUST pay a migration cost: migrate data or saves, reconfigure, relearn core operations |
| Minor Y | You MUST NOT migrate, but you will find new content, mechanics, capabilities, or a change to existing content or values |
| Patch Z | You do not have to do anything; behaviour or performance is corrected or improved, or the data format or security changed |
| Tweak A | You do not have to do anything; the visible effect is limited to details of wording and assets |

### 4.2 Decision Table

This chapter applies only to changes that alter the artifacts distributed to users. Changes that do not alter artifacts are handled by 7.7 and are not governed by this chapter.

Judge by what the user has to do after the update, taking the first matching row from the top:

| What the user has to do after the update | Increment |
| --- | --- |
| Migrate data or saves (including cases where existing data, saves or project files cannot be read by the new version), reconfigure, relearn core operations; or existing content or established usage loses its meaning | Major X |
| Not migrate, but find new content, mechanics, capabilities, or a perceptible change to existing content or values | Minor Y |
| Neither migrate nor find new content, but behaviour or performance is corrected or improved, or the data format or security changed | Patch Z |
| Notice no change in behaviour whatsoever, and the change touches only wording and typos, assets, logs, comments, build configuration shipped with the artifacts, internal implementation or accompanying documentation | Tweak A |

The decision MUST be made by the following five rules:

1. Characterise first. If the change brings the software back to its expected behaviour it is a correction and does not match row 2 of the table, that is, it MUST NOT be treated as a minor merely because existing content or values changed perceptibly; if it establishes a new expectation it is a change. Characterisation precedes row selection. "Expected behaviour" means the behaviour established by an existing official release, or explicitly recorded in release notes and documentation.
2. Match the table from the top and take the first matching row.
3. When one change matches several rows, the higher row MUST be taken, that is, the higher segment.
4. A change that alters no behaviour and is not covered by the closed list in the row for A is judged as Z. The row for A is a closed list, and changes outside it MUST NOT be treated as tweaks.
5. Where the segment still cannot be determined uniquely after characterisation, the higher segment MUST be applied.

The decision table MUST be regarded as the sole basis for ruling on this chapter. Sections 4.3 to 4.6 are applications of it to common cases and establish no further criteria; if they conflict with the table, the table prevails.

### 4.3 Major X

The major MUST be incremented when a change results in any of the following:

1. existing data, saves or project files cannot be read by the new version, and no automatic migration is provided;
2. a restructuring of the core workflow or interface structure that invalidates established habits of use;
3. a change in the software's core positioning that makes existing content or established usage meaningless;
4. the software is remade from scratch.

For items 2 and 3, judge by the objects the user operates: main entry points, keyboard shortcuts, menu hierarchy, and the range of existing content still usable. If these are removed or altered to the point where established habits no longer carry over, the condition is met.

Replacing the underlying engine, refactoring the internal implementation or changing distribution channel does not by itself justify incrementing the major. It increments only when it produces one of the results above.

Announcing a new stage, such as moving from development to stable, does not justify incrementing the major; the official release itself expresses the stage.

### 4.4 Minor Y

The minor MUST be incremented when a change lets users find new content, mechanics or capabilities and does not require them to migrate. Typical cases include new features, mechanics, levels and interactive content, as well as adjustments to existing content or values, provided the user can perceive their effect.

Fixing defects, purely performance work and internal refactoring do not belong to this segment. Rolling a value back to its designed value is a correction and falls under rule 1 of 4.2, that is, the patch.

### 4.5 Patch Z

The patch MUST be incremented when any of the following holds:

1. a user-perceivable defect is fixed;
2. performance is significantly improved while behaviour and content are unchanged; "significantly" is judged by what users can perceive;
3. a security vulnerability is fixed;
4. a behavioural error is corrected without changing the way users operate the software.

A security fix MUST NOT use the tweak, so that users can identify updates they need to obtain first from the version number alone. Its segment is still decided by 4.2: fixing a vulnerability usually lands on the patch; if the fix also makes the data format incompatible, the segment follows that result.

### 4.6 Tweak A

The tweak MUST be incremented when the change touches only typos and grammatical errors, internal assets and resources, logs and comments, build configuration shipped with the artifacts, internal implementation or accompanying documentation.

The tweak MUST NOT be used for features, content, performance, security, data formats, or any user-perceivable behavioural change.

The tweak exists to satisfy two requirements at once: once artifacts change, a new version MUST be released so that version string and content stay in one-to-one correspondence; yet such a change does not deserve a patch number.

### 4.7 Resetting and Incrementing

- When a higher segment is incremented, every lower segment MUST be reset to zero.
- An increment within a segment MUST be exactly one and MUST NOT skip.
- Incrementing the tweak MUST likewise advance it by exactly one.
- Builds that are not publicly released MUST NOT occupy a number in the official sequence and MUST NOT affect the numbering of later official releases.

Skipping is prohibited because a user could no longer infer from the version number how many updates have accumulated, and it would also weaken the claim that a version string maps to exactly one set of artifacts.

| Previous official release | This change | New version (canonical) |
| --- | --- | --- |
| `1.4.1` | Wording and assets only | `1.4.1.1` |
| `1.4.1.1` | Another internal adjustment | `1.4.1.2` |
| `1.4.1.2` | Crash fix | `1.4.2` |
| `1.4.2` | New content | `1.5.0` |
| `1.5.0` | Incompatible save format | `2.0.0` |

### 4.8 Initial Development

While the major is 0, the software is in initial development:

- breaking changes MAY appear at the minor: the changes listed in row 1 of 4.2 are handled as a minor while the major is 0, without incrementing the major;
- the other rows of 4.2, together with the reset and no-skip rules of 4.7, still apply;
- such software SHOULD NOT be described as "complete" or "stable".

`1.0.0` (core 1.0.0.0) SHOULD mark the first official release, indicating that the basic functionality is complete or stable and ready for wide distribution. When moving from 0.y.z to 1.0.0, a data migration path SHOULD be provided, or the incompatibility of existing data SHOULD be stated explicitly.

### 4.9 Borderline Cases

| Change | Segment | Basis |
| --- | --- | --- |
| Fix a typo, update accompanying documentation | A | 4.6 |
| Fix a crash | Z | 4.5 |
| Restore a value that was shipped by mistake to its designed value | Z | 4.2, 4.5 |
| Fix a security vulnerability | Z | 4.5 |
| Load time drops from 8 s to 2 s, behaviour unchanged | Z | 4.5 |
| Internal refactoring, log adjustments | A | 4.6 |
| Add a difficulty mode | Y | 4.4 |
| Lower all weapon damage by 10% | Y | 4.4 |
| Add an interactive scene | Y | 4.4 |
| Rework the save format, old saves unreadable | X | 4.3 |
| Rework the save format, automatic migration, users notice nothing | Z | 4.2 |
| Rework the save format, users must migrate manually | X | 4.3 |
| Replace the engine, save format and behaviour unchanged | A | 4.6 |
| Replace the engine, save format changes but migration is automatic, behaviour unchanged | Z | 4.2 |
| Replace the engine, existing mods all break | X | 4.3 |
| Completely redo the interface layout and interaction | X | 4.3 |
| Adjust CI configuration only, released artifacts unchanged | No increment | 7.7 |

"No increment" here denotes the case in 7.7 and corresponds to no segment.

## 5. Build Labels

*[Normative]*

### 5.1 Syntax and Length

A build label is introduced by a hyphen and consists of 1 to 64 lowercase letters or digits. It is a single segment and contains no dot, hyphen, underscore or uppercase letter.

The limit of 64 is a hard constraint: parsers MUST reject overlong input, see Section 11.

### 5.2 Meaning

A build label annotates a batch of artifacts, saying what that batch is — for example that it comes from an experimental branch, that it is a release candidate, or when it was produced.

A build label is not part of a version and is not that core's official release; artifacts carrying a label still constitute a release and are governed by 7.1, 7.2 and 7.4. Specifically:

- a build label does not participate in precedence (see Section 6);
- a version string carrying a build label has the same precedence as the official release with the same core;
- build labels MUST NOT be relied on to decide which batch is newer. `2.0.0-beta` is not newer than `2.0.0-alpha`, and the two may be entirely unrelated.

### 5.3 Reuse

Build labels MAY be reused freely: the same label may appear on different cores, and one core may have several builds with different labels. `2.0.0.0-alpha` and `3.0.0.0-alpha` are both valid, and their only commonality is the literal label.

### 5.4 Relation to Official Releases

- An official release MUST NOT carry a build label.
- Artifacts carrying a build label MUST NOT be labelled as an official release and SHOULD NOT be offered as the default download.
- Within one product line, a core MAY back at most one official release.
- After an official release has been published, no further build with that core MAY be published, including one carrying a build label. A build label is not a patch channel: if a fix is needed, increment a segment. Withdrawing that official release does not lift this prohibition.
- While a core has no official release, several builds carrying different labels MAY be published for it; they do not consume the core's official-release slot.

### 5.5 Recommended Conventions

*[Informative]*

The meanings below are community conventions. They are not normative and produce no ordering:

| Purpose | Recommended label |
| --- | --- |
| In development | `dev` |
| Closed test | `alpha` |
| Public test | `beta` |
| Release candidate | `rc` |
| Experimental branch | `exp` |
| Build time | A 14-digit UTC timestamp `YYYYMMDDhhmmss`, e.g. `20261103001500` |

### 5.6 Prohibited Uses

- Build labels SHOULD NOT express a change in content, for example `rebuild`, `fixed`, `hotfix` or `patched`. If the content changed, increment a segment, see Section 4.
- Build labels SHOULD NOT be used to ship updates to ordinary users. If a batch of artifacts is to be delivered to ordinary users as an update, a segment MUST be incremented and a new official release published; it MUST NOT be delivered as a labelled build.
- Build labels SHOULD NOT be built into tooling as an ordering key. Depending on the order of `alpha`, `beta` and `rc` means any new label breaks the ordering immediately.

## 6. Precedence and Comparison

*[Normative]*

### 6.1 Algorithm

Comparison happens only within one product line; version numbers of different product lines are not compared, see Section 2.

To compare two version strings a and b:

1. Parse the core (X, Y, Z, A) of each; a missing tweak counts as 0.
2. Compare X, Y, Z and A in order. The first position that differs decides, the numerically greater one having higher precedence.
3. If all four numbers are equal, the two have equal precedence. Build labels take no part in the comparison.
4. Two version strings of equal precedence are the same version, differing only in spelling or being different builds of the same version.

```
compare(a, b):
    pa <- parseCore(a)          # (X, Y, Z, A), missing A = 0
    pb <- parseCore(b)
    for i in 0..3:
        if pa[i] != pb[i]:
            return sign(pa[i] - pb[i])
    return 0                    # build labels take no part
```

### 6.2 Examples

| Relation | Note |
| --- | --- |
| `1.0.0` < `1.0.1` < `1.1.0` < `2.0.0` | Higher segments dominate |
| `9.0.0` < `10.0.0` | Numeric, not lexicographic |
| `1.0.0.1` < `1.0.1` | The tweak is the least significant position |
| `1.4.1` < `1.4.1.1` < `1.4.1.2` < `1.4.2` | Increments within the tweak |
| `1.2.3` = `1.2.3.0` | Two spellings with tweak 0 |
| `2.0.0` = `2.0.0-exp` | Build labels do not affect precedence |
| `1.4.1.1` = `1.4.1.1-rc` | As above |

### 6.3 Deterministic Ordering

*[Informative]*

The specification defines precedence only, not the order among builds of the same core carrying different labels. Tools, however, need a stable result when listing releases or looking for the latest one, so this section gives a deterministic ordering to serve as a tie-break:

1. compare precedence per 6.1;
2. where precedence is equal, a string with a build label sorts before one without;
3. where both carry labels, sort ascending by the byte order of the label.

This ordering is not a normative requirement and MUST NOT be read as indicating which version is newer: it only guarantees that the same input set produces the same output every time. Within the `2.0.0` group, for example, the order is `2.0.0-20261103`, `2.0.0-alpha`, `2.0.0-exp`, `2.0.0`.

Placing unlabelled strings last means that, within one core group, taking the last element yields that core's official release. This is a sorting convenience and carries no meaning: to decide which update something is, precedence per 6.1 MUST be compared first, and labelled builds then excluded from the result.

## 7. Release Discipline

*[Normative]*

### 7.1 A Release

A release is one version string together with one set of artifacts. A release occurs at the moment its artifacts first become available to users.

### 7.2 Immutability

| Object | Requirement |
| --- | --- |
| Official release | MUST be immutable: its artifacts MUST NOT be replaced, added to, removed or repackaged |
| Build carrying a label | SHOULD be immutable |
| Any change in content | MUST be released under a new version string |

### 7.3 Uniqueness

- Within one product line, the core of an official release MUST be unique; one core MAY back exactly one official release.
- One version string MUST map to exactly one set of artifacts.
- While a core has no official release, several builds MAY be published for it under different build labels, but artifacts already published under a name MUST NOT be overwritten.
- Once a core has an official release, no further build with that core MAY be published, see 5.4.

### 7.4 Withdrawal

- A serious defect means one that causes data loss, failure to start, inability to use the software normally after starting, or a security problem.
- Published artifacts MUST NOT be deleted.
- When an official release carries a serious defect, a fix MUST be published under a higher version number.
- A release MAY be marked as withdrawn, but its version string and artifacts MUST be retained, and the release notes MUST state the reason for withdrawal and the affected range of versions.
- A withdrawn version string MUST NOT be re-released.
- Withdrawal acts on the version string, not on the core. Withdrawing a build that carries a label does not affect that core's later official release.

### 7.5 Multiple Channels

- The same version string SHOULD correspond to the same user-perceivable content across all distribution channels.
- Where channel differences concern only store artwork, platform certification, distribution agreements or installation methods — parts unrelated to the content, behaviour or appearance the user encounters while using the software — the same version string MUST be used.
- Where channel differences do alter user-perceivable content — regional cuts or platform-exclusive content, for example — that channel's build MUST use a different version string.
- Channels whose user-perceivable content differs constitute different product lines; their version numbers are not compared with each other and are numbered independently per Section 4.
- Where one version string is rolled out across channels at different times, adding a channel's artifacts does not constitute the addition or removal described in 7.2 and does not create a new official release.

### 7.6 Release Notes

Each release SHOULD provide release notes covering the version string, a summary of changes, whether users must migrate data, whether security fixes are included, and the affected scope.

### 7.7 Changes That Do Not Alter Artifacts

If a change does not alter the artifacts distributed to users — CI configuration, repository documentation or release scripts, for example — no segment needs to be incremented.

If a change does alter the artifacts, a new version string MUST be released even where users cannot perceive the difference.

## 8. Conformance

*[Normative]*

### 8.1 Three Levels

| Level | Meaning |
| --- | --- |
| Format conformance | Every external version string is valid and published in canonical form; every parser duty in Section 3 and 5.1 is satisfied |
| Increment conformance | The choice of segment for every official release follows Section 4 |
| Release conformance | Every normative requirement in Sections 5 and 7 is satisfied, both MUST and MUST NOT |

### 8.2 Declaring Conformance

Adopters SHOULD declare the levels they satisfy using the fixed wording "conforms to ExuoVer 2.0.0 format conformance", "conforms to ExuoVer 2.0.0 increment conformance" and "conforms to ExuoVer 2.0.0 release conformance", which may be combined, as in "conforms to ExuoVer 2.0.0 format and increment conformance".

The three levels are independent: declaring one does not imply declaring another, and a declaration MUST NOT be read as the other levels being satisfied. A level MUST NOT be declared where its requirements are not met.

### 8.3 Partial Conformance

Declaring only some levels is permitted. A project that satisfies format conformance alone is still an adopter of this specification, and its version numbers can be parsed and compared correctly by other tools; that fact MUST NOT be used to suggest that its increment rules also conform.

## 9. Relationship to Semantic Versioning and Migration

*[Informative]*

### 9.1 Compatibility

ExuoVer does not replace Semantic Versioning (SemVer 2.0.0), nor is it a superset of it. The differences are deliberate.

| SemVer 2.0.0 | Valid ExuoVer | Note |
| --- | --- | --- |
| `1.2.3` | Valid | Same canonical form |
| `1.2.3-alpha`, `1.2.3-rc2` | Valid | Falls within the build-label character set |
| `1.2.3-alpha.1` | Invalid | Build labels contain no dot |
| `1.2.3-RC1` | Invalid | Build labels contain no uppercase |
| `1.2.3-alpha-1` | Invalid | Build labels contain no hyphen |
| `1.2.3+build` | Invalid | This specification has no build metadata |
| `01.2.3` | Invalid | Leading zeros are prohibited |

### 9.2 Difference in Ordering

This must be understood before migrating: on the intersection that both specifications accept, ordering does not agree.

In SemVer `1.2.3-alpha` ranks below `1.2.3`; in ExuoVer the two have equal precedence, because build labels take no part in comparison. Under ExuoVer, then, `alpha` is no longer a signal that a version precedes the official release, but merely that this batch carries that label.

If your distribution pipeline depends on pre-release versions sorting backwards, it should be reworked before migrating — for example by using a separate channel instead of relying on version ordering.

### 9.3 Migration Steps

1. Where a build label contains a dot, uppercase, an underscore or a hyphen, or where `+` build metadata is used, rewrite it to a legal label or drop it. This applies only to unpublished version strings; published ones stay as they are per 7.2.
2. Confirm that each core backs exactly one official release; a core with no official release that needs several builds should use different labels, and a core that already has one must not publish further builds.
3. Re-examine the segment chosen for the last several releases against the decision table in Section 4.
4. Fix the canonical form in your build and distribution pipeline, and normalize third-party version strings before parsing them.
5. To declare conformance, use the fixed wording in 8.2 for the levels satisfied.

## 10. Governance

*[Informative]*

- This specification is maintained by MIAR STAFF at https://github.com/MonoIAR/exuover .
- Proposed revisions are submitted as issues and pull requests in that repository, and a new version is published after discussion.
- The specification's own version number follows this specification. This revision is 2.0.0 because the build-label mechanism and the canonical form change the meaning of version numbers, which is a breaking change.
- Each superseded version of the specification is frozen as a copy under `docs/` and is not edited afterwards; the current version is the one at the repository root.
- The Chinese text is the sole normative text; translations in other languages are for reference only, and where a translation conflicts with the Chinese text, the Chinese text prevails.

## 11. Security Considerations

*[Informative]*

- **Length limits**: a build label is capped at 64 characters and each position of the core at 2^63−1, see 3.2 and 5.1. Overlong or out-of-range input is a common vehicle for denial of service, so a parser is best rejecting it while reading rather than allocating first and judging later.
- **Leading zeros**: see 3.4. Several spellings of one number would break the one-to-one correspondence between version string and artifacts; this is a correctness issue, not a style one.
- **Character set**: restricting to ASCII lowercase letters and digits, with no Unicode, avoids ambiguity from homoglyphs and normalization differences when comparing.
- **URLs and file names**: a hyphen needs no escaping in a URL or a file name. This specification has no `+` build metadata and so also avoids escaping `+` as `%2B` in query strings.
- **Sorting implementations**: the precedence in Section 6 is the only order with normative force. The deterministic ordering in 6.3 serves stable output only; using it to judge what is new yields wrong results.

---

## Appendix A. Examples and Counterexamples

*[Informative]*

| Version string | Verdict | Canonical form |
| --- | --- | --- |
| `0.0.0` | Valid | `0.0.0` |
| `1.2.3` | Valid | `1.2.3` |
| `1.2.3.0` | Valid | `1.2.3` |
| `1.2.3.4` | Valid | `1.2.3.4` |
| `10.20.30` | Valid | `10.20.30` |
| `1.2.3-alpha` | Valid | `1.2.3-alpha` |
| `1.2.3-rc2` | Valid | `1.2.3-rc2` |
| `1.2.3-20261103001500` | Valid | `1.2.3-20261103001500` |
| `1.2.3.0-alpha` | Valid | `1.2.3-alpha` |
| `2.0.0-exp` | Valid | `2.0.0-exp` |
| `01.2.3` | Invalid | — |
| `1.02.3` | Invalid | — |
| `1.2.3.00` | Invalid | — |
| `1.2` | Invalid | — |
| `1.2.3.4.5` | Invalid | — |
| `1..3` | Invalid | — |
| `-1.2.3` | Invalid | — |
| `1.2.-3` | Invalid | — |
| `1.2.3-` | Invalid | — |
| `1.2.3-Alpha` | Invalid | — |
| `1.2.3-alpha-1` | Invalid | — |
| `1.2.3-alpha.1` | Invalid | — |
| `1.2.3+build` | Invalid | — |
| `1.2.3-alpha_beta` | Invalid | — |

Two points cannot be shown directly in the table above: a build label longer than 64 characters is an invalid form under 3.2; and whitespace around a version string is handled per 3.3 and is not part of the string.

## Appendix B. Test Vectors

*[Normative]*

Implementers SHOULD verify their parser and comparator against the vectors in this appendix. The vectors below MUST all pass; an implementation that does not pass all of them does not parse or compare conformantly.

### B.1 Equality Groups

Version strings within a group MUST have equal precedence:

| Group | Version strings |
| --- | --- |
| E1 | `1.2.3`, `1.2.3.0` |
| E2 | `2.0.0`, `2.0.0-alpha`, `2.0.0-exp`, `2.0.0-20261103` |
| E3 | `1.4.1.1`, `1.4.1.1-rc` |
| E4 | `0.1.0`, `0.1.0.0`, `0.1.0-dev` |
| E5 | `1.0.0`, `1.0.0.0` |

### B.2 Strictly Increasing Chain

Each adjacent pair MUST increase strictly:

`0.0.1` < `0.1.0` < `0.9.9` < `1.0.0` < `1.0.0.1` < `1.0.1` < `1.1.0` < `1.4.1` < `1.4.1.1` < `1.4.1.2` < `1.4.2` < `2.0.0` < `2.0.0.1` < `2.10.0` < `9.0.0` < `10.0.0` < `11.2.0`

### B.3 Deterministic Ordering

Under the tie-break in 6.3, the order within the `2.0.0` group is:

`2.0.0-20261103`, `2.0.0-alpha`, `2.0.0-exp`, `2.0.0`

This ordering is not part of precedence and exists only to verify that tool output is deterministic.

### B.4 Rejection Cases

A parser MUST reject the following input:

`01.2.3`, `1.2.3.00`, `1.2`, `1..3`, `-1.2.3`, `1.2.3-`, `1.2.3-Alpha`, `1.2.3-alpha.1`, `1.2.3+build`, `9223372036854775808.0.0`, `1.2.3-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`

## Appendix C. Decision Quick Reference

*[Informative]*

1. Will this change alter the artifacts distributed to users? If not, no segment need be incremented (7.7).
2. Do users have to migrate data or saves, reconfigure or relearn core operations, or does existing content lose its meaning? Yes → Major X.
3. Will users find new content, mechanics or capabilities, or a perceptible change to existing content or values? Yes → Minor Y.
4. Is behaviour or performance corrected or improved, or does the change touch the data format or security? Yes → Patch Z.
5. Does the change touch only wording and typos, assets, logs, comments, build configuration shipped with the artifacts, internal implementation or accompanying documentation? Yes → Tweak A.
6. Do you merely want to annotate what this batch of artifacts is? Add a build label and leave the version number alone.

## Appendix D. Mapping from 1.0.0

*[Informative]*

| 1.0.0 clause | 2.0.0 location | Treatment |
| --- | --- | --- |
| Clause 1, format `X.Y.Z.A` | 3.1, 3.2 | Rewritten as an ABNF grammar; the tweak changed from mandatory to omittable |
| Clause 1, example `1.4.1.1` → `1.4.2` | 3.3, 4.7 | Kept; it now holds under the canonical-form rule |
| Clause 2, no change after release | 7.2 | Narrowed: official releases MUST be immutable, others SHOULD be |
| Clause 3, major 0 | 4.8 | Kept and refined |
| Clause 4, `1.0.0.0` as the first official release | 4.8 | Kept; canonical form is `1.0.0` |
| Clause 5, Patch rule | 4.5 | Changed: value adjustments moved to the minor; security fixes became "MUST NOT use the tweak" |
| Clause 6, Minor rule | 4.4 | Kept; now decided by the decision table |
| Clause 8, Tweak rule | 4.6 | Rewritten: the prohibition now covers features, performance, security and data formats |
| Clause 9, suffix | Section 5 | Replaced by the build label: no ordering, reusable; added "official releases carry no label" |
| Clause 10, comparison | Section 6 | Rewritten as a complete algorithm |
| Clause 11, uniqueness | 7.3 | Narrowed and relaxed: official releases MUST be unique; multiple labels on one core changed from prohibited to allowed |
| — | 2, 8, 10, 11 | Added: terminology, conformance, governance, security considerations |

---

## References

*[Informative]*

- **[RFC 2119]** Bradner, S. *Key words for use in RFCs to Indicate Requirement Levels*. BCP 14, 1997.
- **[RFC 8174]** Leiba, B. *Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words*. BCP 14, 2017.
- **[RFC 5234]** Crocker, D., Overell, P. *Augmented BNF for Syntax Specifications: ABNF*. 2008.
- **[SemVer]** Preston-Werner, T. *Semantic Versioning 2.0.0*. https://semver.org
- **[CC-BY-SA-4.0]** Creative Commons. *Attribution-ShareAlike 4.0 International*. https://creativecommons.org/licenses/by-sa/4.0/

## Acknowledgements

*[Informative]*

The four-segment structure and the user-facing stance of 1.0.0 are the foundation of this specification. This revision corrects several mutually conflicting clauses and redefines the purpose of the suffix through the build-label mechanism.

## License

*[Informative]*

This specification is published under the [Creative Commons Attribution-ShareAlike 4.0 International License](../../LICENSE). You are free to copy, distribute and adapt it, provided you give attribution and share alike.
