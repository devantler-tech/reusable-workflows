## ✅⚠️[MegaLinter](https://megalinter.io/9.1.0) analysis: Success with warnings



| Descriptor  |                                               Linter                                                |Files|Fixed|Errors|Warnings|Elapsed time|
|-------------|-----------------------------------------------------------------------------------------------------|----:|----:|-----:|-------:|-----------:|
|✅ ACTION    |[actionlint](https://megalinter.io/9.1.0/descriptors/action_actionlint)                              |   17|     |     0|       0|       0.26s|
|✅ COPYPASTE |[jscpd](https://megalinter.io/9.1.0/descriptors/copypaste_jscpd)                                     |  yes|     |    no|      no|       1.36s|
|✅ JSON      |[jsonlint](https://megalinter.io/9.1.0/descriptors/json_jsonlint)                                    |    3|     |     0|       0|       0.15s|
|✅ JSON      |[prettier](https://megalinter.io/9.1.0/descriptors/json_prettier)                                    |    3|    0|     0|       0|       0.32s|
|✅ JSON      |[v8r](https://megalinter.io/9.1.0/descriptors/json_v8r)                                              |    3|     |     0|       0|       3.39s|
|⚠️ MARKDOWN  |[markdownlint](https://megalinter.io/9.1.0/descriptors/markdown_markdownlint)                        |    1|    0|    30|       0|       0.74s|
|✅ MARKDOWN  |[markdown-table-formatter](https://megalinter.io/9.1.0/descriptors/markdown_markdown_table_formatter)|    1|    0|     0|       0|       0.27s|
|✅ REPOSITORY|[gitleaks](https://megalinter.io/9.1.0/descriptors/repository_gitleaks)                              |  yes|     |    no|      no|       0.09s|
|✅ REPOSITORY|[git_diff](https://megalinter.io/9.1.0/descriptors/repository_git_diff)                              |  yes|     |    no|      no|       0.01s|
|✅ REPOSITORY|[grype](https://megalinter.io/9.1.0/descriptors/repository_grype)                                    |  yes|     |    no|      no|      27.34s|
|✅ REPOSITORY|[secretlint](https://megalinter.io/9.1.0/descriptors/repository_secretlint)                          |  yes|     |    no|      no|       0.47s|
|✅ REPOSITORY|[syft](https://megalinter.io/9.1.0/descriptors/repository_syft)                                      |  yes|     |    no|      no|       1.05s|
|✅ REPOSITORY|[trivy](https://megalinter.io/9.1.0/descriptors/repository_trivy)                                    |  yes|     |    no|      no|       5.02s|
|✅ REPOSITORY|[trivy-sbom](https://megalinter.io/9.1.0/descriptors/repository_trivy_sbom)                          |  yes|     |    no|      no|       0.09s|
|✅ REPOSITORY|[trufflehog](https://megalinter.io/9.1.0/descriptors/repository_trufflehog)                          |  yes|     |    no|      no|       2.25s|
|✅ SPELL     |[lychee](https://megalinter.io/9.1.0/descriptors/spell_lychee)                                       |   24|     |     0|       0|       1.26s|
|✅ YAML      |[prettier](https://megalinter.io/9.1.0/descriptors/yaml_prettier)                                    |   20|    0|     0|       0|       0.63s|
|✅ YAML      |[v8r](https://megalinter.io/9.1.0/descriptors/yaml_v8r)                                              |   20|     |     0|       0|       6.77s|
|✅ YAML      |[yamllint](https://megalinter.io/9.1.0/descriptors/yaml_yamllint)                                    |   20|     |     0|       0|       0.43s|

## Detailed Issues

<details>
<summary>⚠️ MARKDOWN / markdownlint - 30 errors</summary>

```
README.md:33:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:34:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:65:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:66:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:90:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:91:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:115:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:116:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:145:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:146:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:180:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:181:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:197:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:198:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:222:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:223:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:247:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:248:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:275:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:276:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:305:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:306:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:322:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:323:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:347:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:348:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:375:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:376:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:400:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:401:1 MD033/no-inline-html Inline HTML [Element: summary]
```

</details>

See detailed reports in MegaLinter artifacts


Your project could benefit from a custom flavor, which would allow you to run only the linters you need, and thus improve runtime performances. (Skip this info by defining `FLAVOR_SUGGESTIONS: false`)

  - Documentation: [Custom Flavors](https://megalinter.io/9.1.0/custom-flavors/)
  - Command: `npx mega-linter-runner@9.1.0 --custom-flavor-setup --custom-flavor-linters ACTION_ACTIONLINT,COPYPASTE_JSCPD,JSON_JSONLINT,JSON_V8R,JSON_PRETTIER,MARKDOWN_MARKDOWNLINT,MARKDOWN_MARKDOWN_TABLE_FORMATTER,REPOSITORY_GIT_DIFF,REPOSITORY_GITLEAKS,REPOSITORY_GRYPE,REPOSITORY_SECRETLINT,REPOSITORY_SYFT,REPOSITORY_TRIVY,REPOSITORY_TRIVY_SBOM,REPOSITORY_TRUFFLEHOG,SPELL_LYCHEE,YAML_PRETTIER,YAML_YAMLLINT,YAML_V8R`

[![MegaLinter is graciously provided by OX Security](https://raw.githubusercontent.com/oxsecurity/megalinter/main/docs/assets/images/ox-banner.png)](https://www.ox.security/?ref=megalinter)