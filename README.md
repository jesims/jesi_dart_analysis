# JESI Dart Analysis

This package provides lint rules for Dart and Flutter which are used at JESI. For more information on each option,
see the complete [list of options](https://dart.dev/tools/linter-rules).

## Usage

To use the linting options, add a dependency in your `pubspec.yaml`:

```yaml
dev_dependencies:
  # Add Lints for Dart
  lints: '>=1.0.1 <2.0.0'
  # Add Flutter Lints for Flutter
  flutter_lints: '>=1.0.0 <2.0.0'
  jesi_dart_analysis:
    git:
      url: https://github.com/jesi/jesi_dart_analysis.git
      ref: #<tag, branch name, or omit to default to master>
```

Then, create the file `analysis_options.yaml` and add an include statement:

```yaml
# For Dart
include: package:jesi_dart_analysis/analysis_options.yaml

# For Flutter
include: package:jesi_dart_analysis/analysis_options.flutter.yaml
```

This will ensure you always use the latest version of the lints. If you wish to restrict the lint version, specify a
version of `analysis_options.yaml` instead:

```yaml
# For Dart
include: package:jesi_dart_analysis/analysis_options.1.0.0.yaml

# For Flutter
include: package:jesi_dart_analysis/analysis_options.flutter.1.0.0.yaml
```

## Suppressing Lints

There may be cases where specific lint rules are undesirable. Lint rules can be suppressed at the line, file, or project
level.

An example use case for suppressing lint rules at the file level is suppressing the `prefer_single_quotes` in order
to achieve 100% code coverage. This is due to the fact that const constructors are executed before the tests are run,
resulting in no coverage collection.

### Line Level

To suppress a specific lint rule for a specific line of code, use an `ignore` comment directly above the line:

```dart
// ignore: prefer_single_quotes
print("Ignoring standard for this scenario. 'As an Example'");
```

### File Level

To suppress a specific lint rule of a specific file, use an `ignore_for_file` comment at the top of the file:

```dart
// ignore_for_file: prefer_single_quotes

print('This line is fine');
print("This line voids standards");
```

### Project Level

To suppress a specific lint rule for an entire project, modify `analysis_options.yaml`:

```yaml
include: package:jesi_dart_analysis/analysis_options.yaml
linter:
  rules:
    prefer_single_quotes: false
```
