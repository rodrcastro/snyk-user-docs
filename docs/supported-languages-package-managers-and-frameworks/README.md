# Supported languages, package managers, and frameworks

## Overview

Snyk offers support for various languages, customized depending on the Snyk product you are using. These pages focus on Snyk Open Source and Snyk Code.

For information about language support for Snyk Container, see [Supported workloads, container registries, languages, and operating systems](../scan-with-snyk/snyk-container/kubernetes-integration/overview-of-kubernetes-integration/supported-workloads-container-registries-languages-and-operating-systems.md) and [Operating system distributions supported by Snyk Container](../scan-with-snyk/snyk-container/how-snyk-container-works/operating-system-distributions-supported-by-snyk-container.md).

For IaC language support, see [Supported IaC languages, cloud providers, and cloud resources](../scan-with-snyk/snyk-iac/supported-iac-languages-cloud-providers-and-cloud-resources/).

## Supported languages

The following table lists supported languages and the availability of support for using each language with SCM integrations and Snyk CLI, IDE, and CI/CD. Navigate to each language page for more details.

<table><thead><tr><th width="270">Language</th><th width="225">Snyk Open Source</th><th width="210">Snyk Code</th><th data-hidden>SCM support</th><th data-hidden>Snyk CLI, IDE, CI/CD</th></tr></thead><tbody><tr><td><a href="apex.md">Apex</a></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="c-c++/">C/C++</a></td><td>✔️</td><td>✔️</td><td>For Snyk Code</td><td>✔️</td></tr><tr><td><a href="dart-and-flutter.md">Dart and Flutter</a></td><td>✔️</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td></tr><tr><td><a href="elixir.md">Elixir</a></td><td>✔️</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td>✔️</td></tr><tr><td><a href="go/">Go</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="groovy.md">Groovy</a></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td>✔️</td><td></td><td></td></tr><tr><td><a href="java-and-kotlin/">Java and Kotlin</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="javascript/">JavaScript</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href=".net/">.NET</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="php/">PHP</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="python/">Python</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="ruby/">Ruby</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="rust.md">Rust</a></td><td>✔️</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2714">✔️</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td></tr><tr><td><a href="scala/">Scala</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="swift-and-objective-c/">Swift and Objective-C</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="typescript.md">TypeScript</a></td><td>✔️</td><td>✔️</td><td>✔️</td><td>✔️</td></tr><tr><td><a href="vb.net.md">VB NET</a></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖️</span></td><td>✔️</td><td>✔️</td><td>✔️</td></tr></tbody></table>

{% hint style="info" %}
Interfile analysis in Snyk Code is available for all languages supported except Ruby.

For Snyk Open Source, only official releases are tracked. Commits, including into the default branch, are not identified unless included in an official release or tag.&#x20;

For Projects with a package manager, an official release of the package manager is required.&#x20;

For Go and Unmanaged scans (C/C++), an official release or tag on the GitHub repository is required.
{% endhint %}
