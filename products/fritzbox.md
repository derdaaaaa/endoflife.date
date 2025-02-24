---
title: Fritz!Box
category: device

#tags: amazon linux-distribution

# Simple Icons (https://simpleicons.org/) icon slug (optional).
# Remove this property if the icon is not available on Simple Icons.
# As an example, https://simpleicons.org/?q=codemagic links to https://simpleicons.org/icons/codemagic.svg ,
# so the slug is `codemagic` (the SVG filename without extension).
# A list of all slugs is also available on https://github.com/simple-icons/simple-icons/blob/develop/slugs.md .
iconSlug: codemagic

# Main URL for the page (mandatory).
permalink: /fritzbox

releasePolicyLink: https://avm.de/service/status-der-produktunterstuetzung/fritzbox/

# Template to be used to generate a link for the releases (optional).
# Available variables inside the template are:
# - __RELEASE_CYCLE__: will be replaced by the value of `releaseCycle`,
# - __LATEST__: will be replaced by the value of `latest`,
# - __CODENAME__: will be replaced by the optional `codename`.
# You can even use Liquid Templating inside the template, such as:
#   https://godotengine.org/article/maintenance-release-godot-__LATEST__
# Do not use a localized URL (such as one containing en-us) if possible.
changelogTemplate: "https://link/of/the/__RELEASE_CYCLE__/and/__LATEST__/version"

# Template that generates names for every release (optional, default = "__RELEASE_CYCLE__").
# It supports the same variables as changelogTemplate.
releaseLabel: "MoM Timeturner __RELEASE_CYCLE__ (__CODENAME__)"

# The label that will be used alongside releases labelled with `lts: true`
# (optional, default = "<abbr title='Long Term Support'>LTS</abbr>" ).
# Only provide if the product has LTS releases that are not called LTS, but something else.
# Prefer using an HTML abbr tag, if possible.
LTSLabel: "<abbr title='Extra Long Support'>ELS</abbr>"

# Whether the "End of Life" column should be displayed (optional, default = true).
# The value of this property can be set to any string to override the default column label.
eolColumn: Security Support


eolWarnThreshold: 121

activeSupportColumn: Active Support

activeSupportWarnThreshold: 121


releaseColumn: Latest


releaseDateColumn: Released


discontinuedColumn: Discontinued


discontinuedWarnThreshold: 121




# Custom columns configuration (optional).
# Custom columns are columns that will be added to the releases table and populated based on a
# custom release cycle property.
# They can be used for documenting things such as related runtime versions, custom dates that
# cannot be expressed using the default columns, etc.
# Note that the use of a table include (see https://github.com/endoflife-date/endoflife.date/blob/master/products/ansible.md)
# is usually preferred when there is more than two or three custom columns.
customColumns:
  # Name of the custom property in release cycles (mandatory).
  # If the release cycle does not declare this property, the label 'N/A' will be displayed instead.
  # Custom properties follows the camel-case syntax for naming.
  - property: supportedIosVersions

    # Position of the custom column in the table (mandatory).
    # Allowed values are:
    # - after-release-column: this is typically used for documenting related runtime versions
    #   (such as the supported iOS version range for iphone models),
    # - before-latest-column: this is typically used for documenting additional dates
    #   (such as an obsolescence date for an iphone model - https://support.apple.com/en-us/HT201624),
    # - after-latest-column: this is typically used for documenting a corresponding latest version
    #   number (such as the OpenJDK version for https://endoflife.date/azul-zulu).
    # If multiple columns have the same position, the order of the column in the customColumns list
    # will be respected.
    position: after-release-column

    # Label of the custom column (mandatory).
    # It will be displayed in the table header.
    label: iOS

    # A description of what contains the custom column (optional).
    # It will be displayed as a tooltip of the column table header cell.
    description: Supported iOS versions

    # A link that gives more information about what contains the custom column (optional).
    # It will be used to transform the table label to a link.
    link: https://en.wikipedia.org/wiki/IPhone#Models

# Auto-update release configuration (optional).
# This is used for automatically updating `releaseDate`, `latest`, and `latestReleaseDate` for every release.
# Multiple configurations are allowed.
# Please visit https://github.com/endoflife-date/endoflife.date/wiki/Automation for more details.
# The presence of such configuration modifies the product page so that users are informed that existing
# releases are automatically updated with latest versions.
auto:
  # Mark auto-update as being cumulative (optional, default = false).
  # This means that the data won't be deleted before fetching new data.
  # Activating cumulative updates is not recommended for most products, but could be useful for products that:
  # - have a long history of releases that is long to fetch,
  # - have a history of releases that is not available anymore.
  cumulative: true
  methods:
    # Configuration for auto-update based on git.
    # Any valid git clone URL will work, but support for partialClone is necessary
    # (GitHub and GitLab support it).
    # For example, for Apache Maven:
    - git: https://github.com/apache/maven.git

      # Python-compatible regex that defines how the tags above should translate to versions (optional).
      # The default regex can handle versions having at least 2 digits (ex. 1.2) and at most 4 digits (ex. 1.2.3.4),
      # with an optional leading "v"). Use named capturing groups to capture the version or version's parts.
      # Default value should work for most releases of the form a.b, a.b.c or 'v'a.b.c. It should also
      # skip over any special releases (such as nightly,beta,pre,rc...).
      regex: ^v(?<major>\d+)_(?<minor>\d+)_(?<patch>\d{1,3})_?(?<tiny>\d+)?$

      # Python-compatible regex that defines which tags should be excluded (optional).
      regex_exclude: ^v99.99.99$

      # A liquid template using the captured variables from the regex above that renders the final version
      # (optional, default can handle versions having a 'major', 'minor', 'patch' and 'tiny' version).
      # You can use liquid templating here.
      template: ".."

    # Configuration for auto-update based on Docker Hub.
    # The value must be the "owner/repo" combination for a docker hub public image.
    # Use "library" as the owner name for an official docker/community image.
    # For example, for PostgreSQL:
    - docker_hub: library/postgres

    # Configuration for auto-update based on the npm registry.
    # The value must be the package identifier on https://www.npmjs.com .
    # For example, for Vue:
    - npm: vue

    # Configuration for auto-update based on DistroWatch.
    # The value must be the distribution ID. It can be found in the distribution URL.
    # For example, for https://distrowatch.com/index.php?distribution=debian , use "debian".
    - distrowatch: debian

      # The Python-compatible regex used to parse headlines (mandatory).
      # Use named capturing groups to capture the version or version's parts.
      # You can also pass a list of regexes here and matches for any of those will be considered.
      regex: 'Distribution Release: (?P<version>\d+.\d+)'

      # A liquid template using the captured variables from the regex above that renders the final version
      # (optional, default can be found on https://github.com/endoflife-date/release-data/blob/main/src/distrowatch.py#L13 ).
      # You can use liquid templating here.
      template: ""

    # Configuration for auto-update based on Maven Central ( https://search.maven.org ).
    # The value must be the maven coordinates of the artifact, in the form groupId/artifactId.
    # For example, for Apache Tomcat ( https://search.maven.org/artifact/org.apache.tomcat/tomcat ):
    - maven: org.apache.tomcat/tomcat

    # Configuration for auto-update based on a custom script in the release-data repository.
    # The value must be the script name in the release-data repository, without it's '.py' extension.
    - custom: script-name

# A list of identifiers that can be used to detect this product as being used,
# especially by SBOM tooling
identifiers:
  # Each identifier is a way of linking this product to various methods of installing it

  # This is a shorthand to use repology as the source data
  # https://repology.org/project/:package-name-/versions
  # should return a valid list of packages linked to this product.
  - repology: package-name

  # See the PURL spec https://github.com/package-url/purl-spec
  # for details, and avoid packages that are already mentioned on
  # the repology page
  # Common examples would be to use
  # - pkg:os to document operating systems (https://github.com/package-url/purl-spec/pull/161)
  # - pkg:github to link to GitHub pages
  # - pkg:golang/pypi/gem/maven/npm etc for common package managers
  # - pkg:docker for linking to docker images on Docker Hub
  - purl: pkg:package-manager/package-name

# A list of releases, supported or not (mandatory).
# Releases must be sorted from the newest (on top of the list) to the lowest.
# Do not add releases that are not considered "stable" (such as RC/Alpha/Beta/Nightly).
releases:
  # Release range (mandatory, always put in quotes).
  # This is usually major.minor. Do not prefix with "v" or suffix with ".x".
  # This becomes part of our API URL, so try to avoid spaces and use lowercase for words.
  - releaseCycle: "1.2"

    # Name displayed for the release (optional, default = global releaseLabel value).
    # Use this property if you need to override the release label on a per-release basis.
    # You can use templating here, though it is usually not required.
    # Template parameters are the same as the global releaseLabel property.
    releaseLabel: "Timeturner Firebolt (1.2)"

    # Codename of the release (optional, not displayed anywhere by default).
    # It can be used as __CODENAME__ in the releaseLabel and changelogTemplate.
    # It is also returned as-is in the API.
    codename: firebolt

    # Date of the release (optional if releaseDateColumn is false, else mandatory).
    # It should be removed if releaseDateColumn is false.
    # Note that an approximate date is better than no date at all.
    releaseDate: 2017-03-12

    # Whether this is a "LTS" release (optional, default = false).
    # What LTS means may differ from product to product (see LTSLabel above).
    # Only provide for a release that will get much longer support than usual.
    # Alternatively, this can be set to a date when the product is not labeled
    # as LTS when it is released (ex. Angular) or when normal versions are
    # promoted LTS after their release (ex. Jenkins).
    lts: true

    # End of active support date (optional if activeSupportColumn is false, else mandatory).
    # This is where bug fixes usually stop coming in.
    # Use valid dates, and do not add quotes around dates.
    # Alternatively, set to true|false if the date has not been decided yet.
    support: 2018-01-31

    # EOL date (mandatory).
    # This is where all support stops (including security support).
    # In case there is extended/commercial support available, pick the date that would apply to the
    # majority of users (and use the extendedSupport field if necessary).
    # Use valid dates, and do not add quotes around dates.
    # Alternatively, set to true|false the date has not been decided yet.
    eol: 2019-01-01

    # End of extended/commercial support date (optional if extendedSupportColumn is false, else mandatory).
    # Note that extended/commercial support is different from Long-Term Support. Extended/commercial
    # support must be used only when additional support is available after EOL, usually against payment.
    # Use valid dates, and do not add quotes around dates.
    # Alternatively, set to true|false if the date has not been decided yet.
    extendedSupport: 2020-01-01

    # Whether this is a "discontinued" release (optional).
    # Can be set to true/false.
    # Only use if discontinuedColumn is set to true.
    discontinued: true

    # Latest release for the release cycle (optional if releaseColumn is false, else mandatory).
    # Usually this is the release cycle's latest "patch" release.
    # It should be removed if releaseColumn is false.
    # Always add quotes around this value.
    latest: "1.2.3"

    # Latest release date (optional).
    # Use valid dates, and do not add quotes around dates.
    latestReleaseDate: 2022-01-23

    # A link to the changelog for the latest release
    # (optional, default = the URL generated from changelogTemplate if it is provided).
    # Use this if the link is not predictable (i.e. you can't use changelogTemplate),
    # or if the changelogTemplate generated link must be overridden.
    # Do not use a localized URL (such as one containing en-us) if possible.
    # Use the special value 'null' (unquoted) if you want to disable the link for a specific cycle of a
    # product having a changelogTemplate.
    link: https://example.com/news/2021-12-25/release-1.2.3
# In the following markdown section, ensure that all the above are present:
# 1. A one-line statement about what the product is, with a link to the primary website (in a quote).
# 2. A short summary of the release policy, pointing out the EoL policy as well, if available.
# 3. Any additional information that may be of interest.
#
# See also the Guiding Principles on the wiki ( https://github.com/endoflife-date/endoflife.date/wiki/Guiding-Principles )
# for indication of the tone and voice to use for the text.

# Please leave a new line both above and below the triple-dashes.
---

# All the product information text should be under triple-dashes.

# If you are adding any images in the text, they might get blocked due to our CSP.

# So prefer using releaseImage in such cases. Note that images on the same website as releaseImage

# will not be blocked.

> [Time Turner](https://jkrowling.com/time-turner) is a device that powers short-term time travel.

Time-turners are no longer released, and the last known stable release was in HP.5 release.
