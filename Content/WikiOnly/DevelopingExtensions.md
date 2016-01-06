# Developing Extensions



GAMA accepts _extensions_ to the GAML language, defined by external programmers and dynamically loaded by the platform each time it is run. Extensions can represent new built-in species, types, file-types, skills, operators, statements, new control architectures or even types of displays. Other internal structures of GAML will be progressively "opened" to this mechanism in the future: display layers (hardwired for the moment), new types of outputs (hardwired for the moment), scheduling policies (hardwired for the moment), random number generators (hardwired for the moment).
The extension mechanism relies on two complementary techniques:
  * the first one consists in defining the GAML extensions [in a plug-in](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingPlugins.md) (in the OSGI sense, see [here](http://www.eclipse.org/equinox/)) that will be loaded by GAMA at runtime and must "declare" that it is contributing to the platform.
  * the second one is to indicate to GAMA where to look for extensions, using Java annotations that are gathered at compile time (some being also used at runtime) and directly compiled into GAML structures.

The following sections describe this extension process.

  * 1. [Installing the GIT version](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\InstallingGitVersion.md)
  * 2. [Architecture of GAMA](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\GamaArchitecture.md)
  * 3. [Developing a Plugin](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingPlugins.md)
  * 4. [Developing a Skill](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingSkills.md)
  * 5. [Developing a Statement](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingStatements.md)
  * 6. [Developing an Operator](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingOperators.md)
  * 7. [Developing a Type](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingTypes.md)
  * 8. [Developing a Species](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingSpecies.md)
  * 9. [Developing a Control Architecture](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingControlArchitectures.md)
  * 10. [Index of annotations](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingIndexAnnotations.md)
  * 11. [IScope](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\DevelopingExtensions\DevelopingIScope.md)