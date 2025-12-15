## ✅⚠️[MegaLinter](https://megalinter.io/9.1.0) analysis: Success with warnings



| Descriptor  |                                               Linter                                                |Files|Fixed|Errors|Warnings|Elapsed time|
|-------------|-----------------------------------------------------------------------------------------------------|----:|----:|-----:|-------:|-----------:|
|✅ ACTION    |[actionlint](https://megalinter.io/9.1.0/descriptors/action_actionlint)                              |   17|     |     0|       0|       0.32s|
|✅ COPYPASTE |[jscpd](https://megalinter.io/9.1.0/descriptors/copypaste_jscpd)                                     |  yes|     |    no|      no|       1.24s|
|✅ JSON      |[jsonlint](https://megalinter.io/9.1.0/descriptors/json_jsonlint)                                    |    3|     |     0|       0|       0.14s|
|✅ JSON      |[prettier](https://megalinter.io/9.1.0/descriptors/json_prettier)                                    |    3|    0|     0|       0|       0.32s|
|✅ JSON      |[v8r](https://megalinter.io/9.1.0/descriptors/json_v8r)                                              |    3|     |     0|       0|       3.78s|
|⚠️ MARKDOWN  |[markdownlint](https://megalinter.io/9.1.0/descriptors/markdown_markdownlint)                        |    1|    0|    86|       0|       0.76s|
|✅ MARKDOWN  |[markdown-table-formatter](https://megalinter.io/9.1.0/descriptors/markdown_markdown_table_formatter)|    1|    0|     0|       0|       0.28s|
|✅ REPOSITORY|[gitleaks](https://megalinter.io/9.1.0/descriptors/repository_gitleaks)                              |  yes|     |    no|      no|       0.09s|
|✅ REPOSITORY|[git_diff](https://megalinter.io/9.1.0/descriptors/repository_git_diff)                              |  yes|     |    no|      no|       0.01s|
|✅ REPOSITORY|[grype](https://megalinter.io/9.1.0/descriptors/repository_grype)                                    |  yes|     |    no|      no|       27.1s|
|✅ REPOSITORY|[secretlint](https://megalinter.io/9.1.0/descriptors/repository_secretlint)                          |  yes|     |    no|      no|       0.49s|
|✅ REPOSITORY|[syft](https://megalinter.io/9.1.0/descriptors/repository_syft)                                      |  yes|     |    no|      no|       1.27s|
|✅ REPOSITORY|[trivy](https://megalinter.io/9.1.0/descriptors/repository_trivy)                                    |  yes|     |    no|      no|       4.86s|
|✅ REPOSITORY|[trivy-sbom](https://megalinter.io/9.1.0/descriptors/repository_trivy_sbom)                          |  yes|     |    no|      no|        0.1s|
|✅ REPOSITORY|[trufflehog](https://megalinter.io/9.1.0/descriptors/repository_trufflehog)                          |  yes|     |    no|      no|       2.36s|
|✅ SPELL     |[lychee](https://megalinter.io/9.1.0/descriptors/spell_lychee)                                       |   24|     |     0|       0|       1.49s|
|✅ YAML      |[prettier](https://megalinter.io/9.1.0/descriptors/yaml_prettier)                                    |   20|    0|     0|       0|       0.63s|
|✅ YAML      |[v8r](https://megalinter.io/9.1.0/descriptors/yaml_v8r)                                              |   20|     |     0|       0|       6.17s|
|✅ YAML      |[yamllint](https://megalinter.io/9.1.0/descriptors/yaml_yamllint)                                    |   20|     |     0|       0|       0.41s|

## Detailed Issues

<details>
<summary>⚠️ MARKDOWN / markdownlint - 86 errors</summary>

```
README.md:4:81 MD013/line-length Line length [Expected: 80; Actual: 150]
README.md:6:81 MD013/line-length Line length [Expected: 80; Actual: 273]
README.md:8:81 MD013/line-length Line length [Expected: 80; Actual: 91]
README.md:29:81 MD013/line-length Line length [Expected: 80; Actual: 401]
README.md:33:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:34:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:36:81 MD013/line-length Line length [Expected: 80; Actual: 213]
README.md:45:81 MD013/line-length Line length [Expected: 80; Actual: 99]
README.md:55:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:57:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:58:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:59:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:65:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:66:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:68:81 MD013/line-length Line length [Expected: 80; Actual: 157]
README.md:75:81 MD013/line-length Line length [Expected: 80; Actual: 108]
README.md:90:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:91:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:93:81 MD013/line-length Line length [Expected: 80; Actual: 164]
README.md:100:81 MD013/line-length Line length [Expected: 80; Actual: 104]
README.md:115:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:116:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:118:81 MD013/line-length Line length [Expected: 80; Actual: 148]
README.md:125:81 MD013/line-length Line length [Expected: 80; Actual: 95]
README.md:135:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:137:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:138:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:139:81 MD013/line-length Line length [Expected: 80; Actual: 83]
README.md:145:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:146:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:148:81 MD013/line-length Line length [Expected: 80; Actual: 153]
README.md:155:81 MD013/line-length Line length [Expected: 80; Actual: 95]
README.md:164:81 MD013/line-length Line length [Expected: 80; Actual: 131]
README.md:166:81 MD013/line-length Line length [Expected: 80; Actual: 131]
README.md:167:81 MD013/line-length Line length [Expected: 80; Actual: 131]
README.md:168:81 MD013/line-length Line length [Expected: 80; Actual: 131]
README.md:180:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:181:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:183:81 MD013/line-length Line length [Expected: 80; Actual: 165]
README.md:190:81 MD013/line-length Line length [Expected: 80; Actual: 92]
README.md:197:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:198:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:200:81 MD013/line-length Line length [Expected: 80; Actual: 167]
README.md:207:81 MD013/line-length Line length [Expected: 80; Actual: 93]
README.md:222:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:223:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:225:81 MD013/line-length Line length [Expected: 80; Actual: 154]
README.md:232:81 MD013/line-length Line length [Expected: 80; Actual: 86]
README.md:247:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:248:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:250:81 MD013/line-length Line length [Expected: 80; Actual: 143]
README.md:257:81 MD013/line-length Line length [Expected: 80; Actual: 84]
README.md:266:81 MD013/line-length Line length [Expected: 80; Actual: 132]
README.md:268:81 MD013/line-length Line length [Expected: 80; Actual: 132]
README.md:269:81 MD013/line-length Line length [Expected: 80; Actual: 132]
README.md:275:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:276:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:278:81 MD013/line-length Line length [Expected: 80; Actual: 138]
README.md:285:81 MD013/line-length Line length [Expected: 80; Actual: 93]
README.md:295:81 MD013/line-length Line length [Expected: 80; Actual: 96]
README.md:297:81 MD013/line-length Line length [Expected: 80; Actual: 96]
README.md:298:81 MD013/line-length Line length [Expected: 80; Actual: 96]
README.md:299:81 MD013/line-length Line length [Expected: 80; Actual: 96]
README.md:305:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:306:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:308:81 MD013/line-length Line length [Expected: 80; Actual: 148]
README.md:315:81 MD013/line-length Line length [Expected: 80; Actual: 97]
README.md:322:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:323:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:325:81 MD013/line-length Line length [Expected: 80; Actual: 126]
README.md:332:81 MD013/line-length Line length [Expected: 80; Actual: 86]
README.md:347:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:348:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:350:81 MD013/line-length Line length [Expected: 80; Actual: 168]
README.md:357:81 MD013/line-length Line length [Expected: 80; Actual: 100]
README.md:366:81 MD013/line-length Line length [Expected: 80; Actual: 104]
README.md:368:81 MD013/line-length Line length [Expected: 80; Actual: 104]
README.md:369:81 MD013/line-length Line length [Expected: 80; Actual: 104]
README.md:375:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:376:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:378:81 MD013/line-length Line length [Expected: 80; Actual: 131]
README.md:385:81 MD013/line-length Line length [Expected: 80; Actual: 84]
README.md:400:1 MD033/no-inline-html Inline HTML [Element: details]
README.md:401:1 MD033/no-inline-html Inline HTML [Element: summary]
README.md:403:81 MD013/line-length Line length [Expected: 80; Actual: 137]
README.md:410:81 MD013/line-length Line length [Expected: 80; Actual: 85]
```

</details>

See detailed reports in MegaLinter artifacts


Your project could benefit from a custom flavor, which would allow you to run only the linters you need, and thus improve runtime performances. (Skip this info by defining `FLAVOR_SUGGESTIONS: false`)

  - Documentation: [Custom Flavors](https://megalinter.io/9.1.0/custom-flavors/)
  - Command: `npx mega-linter-runner@9.1.0 --custom-flavor-setup --custom-flavor-linters ACTION_ACTIONLINT,COPYPASTE_JSCPD,JSON_JSONLINT,JSON_V8R,JSON_PRETTIER,MARKDOWN_MARKDOWNLINT,MARKDOWN_MARKDOWN_TABLE_FORMATTER,REPOSITORY_GIT_DIFF,REPOSITORY_GITLEAKS,REPOSITORY_GRYPE,REPOSITORY_SECRETLINT,REPOSITORY_SYFT,REPOSITORY_TRIVY,REPOSITORY_TRIVY_SBOM,REPOSITORY_TRUFFLEHOG,SPELL_LYCHEE,YAML_PRETTIER,YAML_YAMLLINT,YAML_V8R`

[![MegaLinter is graciously provided by OX Security](https://raw.githubusercontent.com/oxsecurity/megalinter/main/docs/assets/images/ox-banner.png)](https://www.ox.security/?ref=megalinter)