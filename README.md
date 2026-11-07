# Built North Coding Standards

WordPress coding standards for Built North projects, extending WPCS with modern PHP practices.

## Overview

This package provides a consistent set of coding standards for all Built North WordPress projects. It extends the WordPress Coding Standards (WPCS) while allowing modern PHP features and PSR-4 autoloading.

## Installation

Add to your project via Composer:

```bash
composer require --dev builtnorth/coding-standards
```

## Usage

### Basic Usage

Create a `phpcs.xml` file in your project root:

```xml
<?xml version="1.0"?>
<ruleset name="My Project">
    <description>Coding standards for my project</description>
    
    <!-- Use Built North standards -->
    <rule ref="BuiltNorth"/>
    
    <!-- Project-specific text domain -->
    <rule ref="WordPress.WP.I18n">
        <properties>
            <property name="text_domain" type="array">
                <element value="my-text-domain"/>
            </property>
        </properties>
    </rule>
</ruleset>
```

### Running the Standards

```bash
# Check your code
vendor/bin/phpcs

# Fix auto-fixable issues
vendor/bin/phpcbf

# Check specific file or directory
vendor/bin/phpcs src/

# Check with specific standard
vendor/bin/phpcs --standard=BuiltNorth
```

## What's Included

### Base Standards
- WordPress Coding Standards (WPCS) 3.0+
- PHP Compatibility checks for PHP 8.1+
- PSR-1/PSR-2 file structure rules

### Modern PHP Features Allowed
- ✅ Short array syntax `[]`
- ✅ Short ternary operator `?:`
- ✅ Namespaces and PSR-4 autoloading
- ✅ Modern PHP 8.1+ features

### Excluded WordPress Rules
- File naming conventions (we use PSR-4)
- Yoda conditions requirement
- File comment requirements
- Overly strict comment punctuation

### File Exclusions
Automatically excludes from scanning:
- `/vendor/`
- `/node_modules/`
- `/build/` and `/dist/`
- `*.min.js` and `*.min.css`
- WordPress core files
- Test bootstrap files

## Customization

### Adding Project-Specific Rules

Your project's `phpcs.xml` can add additional rules:

```xml
<rule ref="BuiltNorth"/>

<!-- Add project-specific rules -->
<rule ref="WordPress.WP.EnqueuedResourceParameters"/>

<!-- Or exclude specific rules -->
<rule ref="BuiltNorth">
    <exclude name="WordPress.NamingConventions.PrefixAllGlobals"/>
</rule>
```

### Setting Prefixes for Global Functions

```xml
<rule ref="WordPress.NamingConventions.PrefixAllGlobals">
    <properties>
        <property name="prefixes" type="array">
            <element value="my_prefix"/>
            <element value="MyNamespace"/>
        </property>
    </properties>
</rule>
```

## Integration with CI/CD

### GitHub Actions Example

```yaml
- name: Install dependencies
  run: composer install

- name: Run PHPCS
  run: vendor/bin/phpcs --report=checkstyle | cs2pr
```

### Pre-commit Hook

Add to `.git/hooks/pre-commit`:

```bash
#!/bin/bash
vendor/bin/phpcs --filter=GitStaged
```

## Philosophy

Our coding standards aim to:

1. **Embrace Modern PHP**: Use PHP 8.1+ features while maintaining WordPress compatibility
2. **Prioritize Readability**: Code should be self-documenting with clear naming
3. **Support PSR-4**: Use modern autoloading instead of WordPress file naming
4. **Balance Strictness**: Enforce important standards without being pedantic
5. **Enable Consistency**: Same standards across all Built North projects

## Requirements

- PHP >= 8.1
- Composer
- WordPress project (for context-aware rules)

## Contributing

To contribute to these standards:

1. Clone the repository
2. Make your changes to `BuiltNorth/ruleset.xml`
3. Test with real projects
4. Submit a pull request with reasoning for changes

## License

MIT