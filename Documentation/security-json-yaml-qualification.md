# JSON/YAML dependency candidate — not release-qualified

This candidate pins Newtonsoft.Json 13.0.4 and direct YamlDotNet 6.0.0 across
package declarations, DLL paths and Newtonsoft binding redirects. The YAML
caller uses the builder and IParser API while retaining the boolean converter.
Existing framework targets and public APIs remain unchanged.

The existing net45 assets exist in the exact packages. The portable HintPath is
an existing Newtonsoft netstandard1.0 candidate asset, **not completed
Profile111 qualification**. Its old portable directory does not exist in
13.0.4. Do not merge or release this candidate until the Profile111 compilation,
dependency resolution and actual consumer behavior are qualified. No target
has been dropped and no old DLL path has been kept behind a new manifest.

Bounded local evidence uses four complete repository caller source files and
the actual public assemblies under .NET10 with outbound network denied. With
compatible assets, the baseline accepts excessive JSON depth and instantiates
a harmless tagged YAML type; the candidate rejects both while preserving the
normal-input controls. This is not .NETFramework/portable/xproj evidence.
Legacy DLL execution on that host requires System.Security.Permissions;
compatible-asset compilation also retains assembly-unification warnings.
Neither is waived by these tests.

The same four candidate caller files also compile against Microsoft's official
net45 reference assemblies with warnings treated as errors. This establishes
their net45 API compilation, not CLR4 execution or a whole-project build.

Before release, qualify the remaining net45 project compilation
and actual CLR4/.NETFramework4.8+ execution; Profile111 compilation using the
official Portable Library targeting pack; the preserved netstandard1.1/1.5
targets; restored dependency graphs; existing generator, client serialization
and package tests; and packaged DLL versions/strong-name compatibility. A
passing subset does not establish the separate 40 project.json / 40 xproj
coverage or retire the four known high-version groups.

Advisories: GHSA-5crp-9r3c-p9vr (Newtonsoft fix floor13.0.1) and
GHSA-rpch-cqj9-h65r (YamlDotNet fix floor5.0.0). The selected versions exceed
those floors; this is not a current whole-graph security or lifecycle claim.
