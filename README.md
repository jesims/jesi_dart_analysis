# JESI Dart Analysis

This package provides lint rules for Dart and Flutter which are used at JESI.

For more information on each option, see the complete [list of options](https://dart.dev/tools/linter-rules).

For more information about the core libraries, see the related package:

- [Dart Lints](https://pub.dev/packages/lints)
- [Flutter Lints](https://pub.dev/packages/flutter_lints)

## Usage

To use the linting options, add a dependencies into your `pubspec.yaml`:

```yaml
dev_dependencies:
  lints: ^1.0.1 # Add for Dart
  # flutter_lints: ^1.0.0 # Add for Flutter
  jesi_dart_analysis:
    git:
      url: https://github.com/jesims/jesi_dart_analysis.git
      ref: #<tag, branch name, or omit to default to master>
```

Then, create the file `analysis_options.yaml` and add an include statement:

```yaml
# For Dart
include: package:jesi_dart_analysis/analysis_options.yaml

# For Flutter
include: package:jesi_dart_analysis/analysis_options.flutter.yaml
```

This will ensure you always use the latest version of the lints.

## Suppressing Lints

There may be cases where specific lint rules are undesirable. Lint rules can be suppressed at the line, file, or project
level.

### Line Level

To suppress a specific lint rule for a specific line of code, use an `ignore` comment directly above the line.
[Read More](https://dart.dev/guides/language/analysis-options#suppressing-rules-for-a-line-of-code)

```dart
// ignore: uri_does_not_exist
import '/__generated__/main.gql.dart';
import 'collection_extensions.dart';
```

### File Level

To suppress a specific lint rule of a specific file, use an `ignore_for_file` comment at the top of the file.
[Read More](https://dart.dev/guides/language/analysis-options#suppressing-rules-for-a-file)

```dart
// ignore_for_file: uri_does_not_exist
import '/__generated__/main.gql.dart';
import '/__generated__/another.gql.dart';
```

### Project Level

To suppress a specific lint rule for an entire project, modify `analysis_options.yaml`.
[Read More](https://dart.dev/guides/language/analysis-options#disabling-individual-rules)

```yaml
include: package:jesi_dart_analysis/analysis_options.yaml
linter:
  rules:
    prefer_single_quotes: false
```

## Maintaining

- Follow [Semantic Versioning](https://semver.org/)
- Update the `CHANGELOG.md` accordingly
- When updating linter rules, ensure the rule is changed in both `analysis_options.yaml` and
  `analysis_options.flutter.yaml`. _Unless the rule pertains exclusively to either Flutter or Dart._
- After merging, create (and push) a new `tag` for the version
  1. `git tag x.x.x`
  1. `git push -u --tags`

## Future Work

- Consider CI/CD Automation
- If package maintenance starts becoming a lot of effort maintaining two analysis files, consider creating a build
  script to generate, or lint, the YAML files as part of a `pre-commit` or `pre-push` hook.
