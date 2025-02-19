# Changelog

## v2.4.8 (2022-07-29)

### Bug fixes

- feat: support application level extensions (#9923)
- feat: support multiple extensions per resource group/kind (#9834)
- fix: extensions is not loading for ConfigMap/Pods (#10010)
- fix: upgrade moment from 2.29.2 to 2.29.3 (#9330)
- fix: skip redirect url validation when it's the base href (#10058) (#10116)
- fix: avoid CVE-2022-28948 (#10093)
- fix: Set HOST_ARCH for yarn build from platform (#10018)

### Other changes

- chore(deps): bump moment from 2.29.3 to 2.29.4 in /ui (#9897)
- docs: add OpenSSH breaking change notes (#10104)
- chore: update parse-url (#10101)
- docs: add api field example in the appset security doc (#10087)
- chore: update redis to 7.0.4 avoid CVE-2022-30065 (#10059)
- docs: add argocd-server grpc metric usage (#10007)
- chore: upgrade Dex to 2.32.0 (#10036) (#10042)
- chore: update redis to avoid CVE-2022-2097 (#10031)
- chore: update haproxy to 2.0.29 for redis-ha (#10045)

## v2.4.7 (2022-07-18)

### Bug fixes

fix: Support files in argocd.argoproj.io/manifest-generate-paths annotation (#9908)
fix: terminal websocket write lock to avoid races (#10011)
fix: updated all a tags to Link tags in app summary (#9777)
fix: e2e test to use func from clusterauth instead creating one with old logic (#9989)
fix: add missing download CLI tool URL response for ppc64le, s390x (#9983)

### Other

chore: upgrade parse-url to avoid SNYK-JS-PARSEURL-2936249 (#9826)
docs: use quotes to emphasize that ConfigMap value is a string (#9995)
docs: document directory app include/exclude fields (#9997)
docs: simplify Docker toolchain docs (#9966) (#10006)
docs: supported versions (#9876)

## v2.4.6 (2022-07-12)

### Features

* feat: Treat connection reset as a retryable error (#9739)

### Bug fixes

* fix: 'unexpected reserved bits' breaking web terminal (#9605) (#9895)
* fix: argocd login just hangs on 2.4.0 #9679 (#9935)
* fix: CMP manifest generation fails with ENHANCE_YOUR_CALM if over 40s (#9922)
* fix: NotAfter is not set when ValidFor is set (#9911)
* fix: add missing download CLI tool link for ppc64le, s390x (#9649)
* fix: Check tracking annotation for being self-referencing (#9791)
* fix: Make change of tracking method work at runtime (#9820)
* fix: argo-cd git submodule is using SSH auth instead of HTTPs (#3118) (#9821)

### Other

* docs: fix typo in Generators-Git.md (#9949)
* docs: add terminal documentation (#9948)
* test: Use dedicated multi-arch workloads in e2e tests (#9921)
* docs: Adding blank line so list is formatted correctly (#9880)
* docs: small fix for plugin stream filtering (#9871)
* docs: Document the possibility of rendering Helm charts with Kustomize (#9841)
* docs: getting started notes on self-signed cert (#9429) (#9784)
* test: check for error messages from CI env (#9953)

## v2.4.5 (2022-07-12)

### Security fixes

* HIGH: Certificate verification is skipped for connections to OIDC providers ([GHSA-7943-82jg-wmw5](https://github.com/argoproj/argo-cd/security/advisories/GHSA-7943-82jg-wmw5))
* LOW: A leaked API server encryption key can allow XSS for SSO users ([GHSA-pmjg-52h9-72qv](https://github.com/argoproj/argo-cd/security/advisories/GHSA-pmjg-52h9-72qv))

### Potentially-breaking changes

The fix for GHSA-7943-82jg-wmw5 enables TLS certificate validation by default for connections to OIDC providers. If
connections to your OIDC provider fails validation, SSO will be broken for your Argo CD instance. You should test 2.4.5
before upgrading it to production. From the new documentation:

> By default, all connections made by the API server to OIDC providers (either external providers or the bundled Dex
> instance) must pass certificate validation. These connections occur when getting the OIDC provider's well-known
> configuration, when getting the OIDC provider's keys, and  when exchanging an authorization code or verifying an ID
> token as part of an OIDC login flow.
>
> Disabling certificate verification might make sense if:
> * You are using the bundled Dex instance **and** your Argo CD instance has TLS configured with a self-signed certificate
    >   **and** you understand and accept the risks of skipping OIDC provider cert verification.
> * You are using an external OIDC provider **and** that provider uses an invalid certificate **and** you cannot solve
    >   the problem by setting `oidcConfig.rootCA` **and** you understand and accept the risks of skipping OIDC provider cert
    >   verification.
>
> If either of those two applies, then you can disable OIDC provider certificate verification by setting
> `oidc.tls.insecure.skip.verify` to `"true"` in the `argocd-cm` ConfigMap.

### Bug fixes

* fix: webhook typo in case of error in GetManifests (#9671)

## v2.4.4 (2022-07-07)

### Bug fixes

- fix: missing path segments for git file generator (#9839)
- fix: make sure api server informer does not stop after setting change (#9842)
- fix: support resource logs and exec (#9833)
- fix: configurable CMP tar exclusions (#9675) (#9789)
- fix: prune any deleted refs before fetching (#9504)

### Other

- test: Remove circular symlinks from testdata (#9886)
- docs: custom secret must be labeled (#9835)
- docs: update archlinux install with official package (#9718)
- docs: explain rightmost git generator path parameter behavior (#9799)

## v2.4.3 (2022-06-27)

### Bug fixes

- fix: respect OIDC providers' supported token signing algorithms (#9433) (#9761)
- fix websockets for terminal not working on subPath (#9795)
- fix: avoid closing and re-opening port of api server settings change (#9778)
- fix: [ArgoCD] Fixing webhook typo in case of error in GetManifests (#9671)
- fix: overrides should not appear in the manifest cache key (#9601)

## v2.4.2 (2022-06-21)

### Bug fixes

* fix: project filter (#9651) (#9709)
* fix: broken symlink in Dockerfile (#9674)
* fix: updated baseHRefRegex to perform lazy match (#9724)
* fix: updated config file permission requirements for windows (#9666)

### Other

* docs: Update sync-options.md (#9687)
* test/remote: Allow override of base image (#9734)

## v2.4.1 (2022-06-21)

### Security fixes

* CRITICAL: External URLs for Deployments can include javascript ([GHSA-h4w9-6x78-8vrj](https://github.com/argoproj/argo-cd/security/advisories/GHSA-h4w9-6x78-8vrj))
* HIGH: Insecure entropy in PKCE/Oauth2/OIDC params ([GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v))
* MODERATE: DoS through large directory app manifest files ([GHSA-jhqp-vf4w-rpwq](https://github.com/argoproj/argo-cd/security/advisories/GHSA-jhqp-vf4w-rpwq))
* MODERATE: Symlink following allows leaking out-of-bounds YAML files from Argo CD repo-server ([GHSA-q4w5-4gq2-98vm](https://github.com/argoproj/argo-cd/security/advisories/GHSA-q4w5-4gq2-98vm))

### Potentially-breaking changes

From the [GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v) description:

> The patch introduces a new `reposerver.max.combined.directory.manifests.size` config parameter, which you should tune before upgrading in production. It caps the maximum total file size of .yaml/.yml/.json files in directory-type (raw manifest) Applications. The default max is 10M per Application. This max is designed to keep any single app from consuming more than 3G of memory in the repo-server (manifests consume more space in memory than on disk). The 300x ratio assumes a maliciously-crafted manifest file. If you only want to protect against accidental excessive memory use, it is probably safe to use a smaller ratio.
>
> If your organization uses directory-type Applications with very many manifests or very large manifests then check the size of those manifests and tune the config parameter before deploying this change to production. When testing, make sure to do a "hard refresh" in either the CLI or UI to test your directory-type App. That will make sure you're using the new max logic instead of relying on cached manifest responses from Redis.

### Other

* test: directory app manifest generation (#9503)
* chore: Implement tests to validate aws auth retry (#9627)
* chore: Implement a retry in aws auth command (#9618)
* test: Remove temp directories from repo server tests (#9501)
* test: Make context tests idempodent (#9502)
* test: fix plugin var test for OSX (#9590)
* docs: Document how to deploy from the root of the git repository (#9632)
* docs: added environment variables documentation (#8680)

## v2.4.0 (2022-06-10)

### Web Terminal In Argo CD UI

Feature enables engineers to start a shell in the running application container without leaving the web interface. Just find the required Kubernetes
Pod using the Application Details page, click on it and select the Terminal tab. The shell starts automatically and enables you to execute the required
commands, and helps to troubleshoot the application state.

### Access Control For Pod Logs & Web Terminal

Argo CD is used to manage the critical infrastructure of multiple organizations, which makes security the top priority of the project. We've listened to
your feedback and introduced additional access control settings that control access to Kubernetes Pod logs and the new Web Terminal feature.

#### Pod Logs UI

Since 2.4.7, the LOGS tab in pod view is visible in the UI only for users with explicit allow get logs policy.

#### Known pod logs UI issue prior to 2.4.7

Upon pressing the "LOGS" tab in pod view by users who don't have an explicit allow get logs policy, the red "unable to load data: Internal error" is received in the bottom of the screen, and "Failed to load data, please try again" is displayed.

### OpenTelemetry Tracing Integration

The new feature allows emitting richer telemetry data that might make identifying performance bottlenecks easier. The new feature is available for argocd-server
and argocd-repo-server components and can be enabled using the --otlp-address flag.

### Power PC and IBM Z Support

The list of supported architectures has been expanded, and now includes IBM Z (s390x) and PowerPC (ppc64le). Starting with the v2.4 release the official quay.io
repository is going to have images for amd64, arm64, ppc64le, and s390x architectures.

### Other Notable Changes

Overall v2.4 release includes more than 300 hundred commits from nearly 90 contributors. Here is a short sample of the contributions:

* Enforce the deployment to remote clusters only
* Native support of GCP authentication for GKE
* Secured Redis connection
* ApplicationSet Gitea support

## v2.3.7 (2022-07-29)

### Notes

This is mainly a security related release and updates compatibility with Kubernetes 1.24.

**Attention:** The base image for 2.3.x reached end-of-life on July 14, 2022. This release upgraded the base image to Ubuntu 22.04 LTS. The change should have no effect on the majority of users. But if any of your git providers only supports now-deprecated key hash algorithms, then Application syncing might break. See the [2.2-to-2.3 upgrade notes](https://argo-cd.readthedocs.io/en/latest/operator-manual/upgrading/2.2-2.3/#support-for-private-repo-ssh-keys-using-the-sha-1-signature-hash-algorithm-is-removed-in-237) for details and workaround instructions.

### Bug fixes

- fix: skip redirect url validation when it's the base href (#10058) (#10116)
- fix: upgrade moment from 2.29.2 to 2.29.3 (#9330)
- fix: avoid CVE-2022-28948 (#10093)
- fix: use serviceaccount name instead of struct (#9614)
- fix: create serviceaccount token for v1.24 clusters (#9546)

### Other changes

- test: Remove cluster e2e tests not intended for release-2.3
- test: Remove circular symlinks from testdata (#9886)
- chore(deps): bump moment from 2.29.3 to 2.29.4 in /ui (#9897)
- chore: upgrade moment to latest version to fix CVE (#9005)
- chore: move dependencies to dev dependencies (#8541)
- docs: add OpenSSH breaking change notes (#10104)
- chore: update parse-url (#10101)
- chore: upgrade base image to 22.04 (#10103)
- docs: simplify Docker toolchain docs (#9966) (#10006)
- chore: update redis to 6.2.7 avoid CVE-2022-30065/CVE-2022-2097 (#10062)
- chore: upgrade Dex to 2.32.0 (#10036) (#10042)
- chore: update haproxy to 2.0.29 for redis-ha (#10045)
- test: check for error messages from CI env (#9953)

## v2.3.6 (2022-07-12)

### Security fixes

* HIGH: Certificate verification is skipped for connections to OIDC providers ([GHSA-7943-82jg-wmw5](https://github.com/argoproj/argo-cd/security/advisories/GHSA-7943-82jg-wmw5))
* LOW: A leaked API server encryption key can allow XSS for SSO users ([GHSA-pmjg-52h9-72qv](https://github.com/argoproj/argo-cd/security/advisories/GHSA-pmjg-52h9-72qv))

### Potentially-breaking changes

The fix for GHSA-7943-82jg-wmw5 enables TLS certificate validation by default for connections to OIDC providers. If
connections to your OIDC provider fails validation, SSO will be broken for your Argo CD instance. You should test 2.3.6
before upgrading it to production. From the new documentation:

> By default, all connections made by the API server to OIDC providers (either external providers or the bundled Dex
> instance) must pass certificate validation. These connections occur when getting the OIDC provider's well-known
> configuration, when getting the OIDC provider's keys, and  when exchanging an authorization code or verifying an ID
> token as part of an OIDC login flow.
>
> Disabling certificate verification might make sense if:
> * You are using the bundled Dex instance **and** your Argo CD instance has TLS configured with a self-signed certificate
    >   **and** you understand and accept the risks of skipping OIDC provider cert verification.
> * You are using an external OIDC provider **and** that provider uses an invalid certificate **and** you cannot solve
    >   the problem by setting `oidcConfig.rootCA` **and** you understand and accept the risks of skipping OIDC provider cert
    >   verification.
>
> If either of those two applies, then you can disable OIDC provider certificate verification by setting
> `oidc.tls.insecure.skip.verify` to `"true"` in the `argocd-cm` ConfigMap.

### Bug fixes

* fix: webhook typo in case of error in GetManifests (#9671)

## v2.3.5 (2022-06-21)

### Security fixes

* CRITICAL: External URLs for Deployments can include javascript ([GHSA-h4w9-6x78-8vrj](https://github.com/argoproj/argo-cd/security/advisories/GHSA-h4w9-6x78-8vrj))
* HIGH: Insecure entropy in PKCE/Oauth2/OIDC params ([GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v))
* MODERATE: DoS through large directory app manifest files ([GHSA-jhqp-vf4w-rpwq](https://github.com/argoproj/argo-cd/security/advisories/GHSA-jhqp-vf4w-rpwq))
* MODERATE: Symlink following allows leaking out-of-bounds YAML files from Argo CD repo-server ([GHSA-q4w5-4gq2-98vm](https://github.com/argoproj/argo-cd/security/advisories/GHSA-q4w5-4gq2-98vm))

### Potentially-breaking changes

From the [GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v) description:

> The patch introduces a new `reposerver.max.combined.directory.manifests.size` config parameter, which you should tune before upgrading in production. It caps the maximum total file size of .yaml/.yml/.json files in directory-type (raw manifest) Applications. The default max is 10M per Application. This max is designed to keep any single app from consuming more than 3G of memory in the repo-server (manifests consume more space in memory than on disk). The 300x ratio assumes a maliciously-crafted manifest file. If you only want to protect against accidental excessive memory use, it is probably safe to use a smaller ratio.
>
> If your organization uses directory-type Applications with very many manifests or very large manifests then check the size of those manifests and tune the config parameter before deploying this change to production. When testing, make sure to do a "hard refresh" in either the CLI or UI to test your directory-type App. That will make sure you're using the new max logic instead of relying on cached manifest responses from Redis.

### Bug fixes

* fix: missing Helm params (#9565) (#9566)

### Other

* test: directory app manifest generation (#9503)
* chore: eliminate go-mpatch dependency (#9045)
* chore: Make unit tests run on platforms other than amd64 (#8995)
* chore: remove obsolete repo-server unit test (#9559)
* chore: update golangci-lint (#8988)
* fix: test race (#9469)
* chore: upgrade golangci-lint to v1.46.2 (#9448)
* test: fix ErrorContains (#9445)

## v2.3.4 (2022-05-18)

### Security fixes

- CRITICAL: Argo CD will trust invalid JWT claims if anonymous access is enabled (https://github.com/argoproj/argo-cd/security/advisories/GHSA-r642-gv9p-2wjj)
- LOW: Login screen allows message spoofing if SSO is enabled (https://github.com/argoproj/argo-cd/security/advisories/GHSA-xmg8-99r8-jc2j)
- MODERATE: Symlink following allows leaking out-of-bound manifests and JSON files from Argo CD repo-server (https://github.com/argoproj/argo-cd/security/advisories/GHSA-6gcg-hp2x-q54h)

### Bug Fixes

- fix: Fix docs build error (#8895)
- fix: fix broken monaco editor collapse icons (#8709)
- chore: upgrade to go 1.17.8 (#8866) (#9004)
- fix: allow cli/ui to follow logs (#8987) (#9065)

## v2.3.3 (2022-03-29)

- fix: prevent excessive repo-server disk usage for large repos (#8845) (#8897)
- fix: Set QPS and burst rate for resource ops client (#8915)

## v2.3.2 (2022-03-22)

- fix: application resource APIs must enforce project restrictions

## v2.3.1 (2022-03-10)

- fix: Retry checkbox unchecked unexpectedly; Sync up with YAML (#8682) (#8720)
- chore: Bump stable version of application set addon (#8744)
- fix: correct jsonnet paths resolution (#8721)
- fix(ui): Applications page incorrectly resets to tiles view. Fixes #8702 (#8718)

## v2.3.0 (2022-03-05)

### Argo CD ApplicationSet and Notifications are now part of Argo CD

Two popular [Argoproj Labs](https://github.com/argoproj-labs) projects [Argo CD ApplicationSet](https://github.com/argoproj/applicationset) and
[Argo CD Notifications](https://github.com/argoproj-labs/argocd-notifications) are now part of Argo CD! The default Argo CD installation manifests now
bundle both projects out of the box. Going forward you can expect more tightened integration of these projects into Argo CD.

### New sync and diff strategies

Users can now configure the Application resource to instruct Argo CD to consider the ignore difference setup during the sync process.
In order to do so, add the new sync option RespectIgnoreDifferences=true in the Application resource. Once the sync option is added,
Argo CD won't change ignored fields during the syncing process.

Configuring ignored fields is also easier now. Instead of listing fields one by one users can now leverage the 
managedFields metadata to instruct Argo CD about trusted managers and automatically ignore any fields owned by them. A new diff customization
(managedFieldsManagers) is now available allowing users to specify managers the application should trust and to ignore all fields owned by those managers.
Read more about these changes at [New sync and diff strategies in ArgoCD](https://blog.argoproj.io/new-sync-and-diff-strategies-in-argocd-44195d3f8b8c) blog post.

### ARM Images

An officially supported ARM 64 image is now available. Enjoy running Argo CD on your Raspberry Pi! Additionally, the image size was reduced by nearly ~50%
and is only 200MB now. The ARM version of `argocd` CLI is also available and published as a Github release artifact.

### Compact Tree View And Click Application Navigation

The application details page now supports compact application resources tree visualization. Using the "Group Nodes" button, you can collapse the similar resources
into a single group node to remove the clutter and make it easier to understand the state of application resources. You still can get detailed information about the collapsed resources by clicking on the group node. The list of collapsed resources will be available in a sliding panel. Compact resource tree is still too big?
You can use the zoom in and zoom out feature to make it smaller - or even larger!

You no longer need to move back and forth between the application details page and the application list page. Instead you can navigate directly to the required application by clicking the search icon in the application details page title.

### Upgraded Config Management Tools

Both bundled Helm and Kustomize binaries have been upgraded to the latest versions. Kustomize has been upgraded from 4.2.0 to 4.4.1 and Helm has been upgraded from 3.7.1 to 3.8.0.

### Bug Fixes and Performance Enhancements

* Config management tools enhancements:
* The skipCrds flag and ability to ignore missing values files for Helm (#8012, #8003)
* Additional environment variables for Kustomize (#8096)
* Argo CD CLI follows the XDG Base directory standard (#7638)
* Redis is no longer used during SSO login (#8241)


### Features

- feat: Add app list and details page views to navigation history (#7776) (#7937)
- feat: Add skipCrds flag for helm charts (#8012)
- feat: Add visual indicator for newly created pods (#8006)
- feat: Added a new Helm option ignoreMissingValueFiles (#7767) (#8003)
- feat: Allow configuring system wide ignore differences for all resources (#8224)
- feat: Allow escaping dollar in Envsubst (#7961)
- feat: Allow external links on Application (#3487) (#8231)
- feat: Allow selecting application on detail page (#8176)
- feat: Bundle applicationset-controller with argocd (#8148)
- feat: Enable specifying root ca for oidc (#6712)
- feat: Expose ARGOCD_APP_NAME to the `kustomize build` command (#8096)
- feat: Ignore differences owned by trusted managers from managedFields (#7869)
- feat: New sync option to use ignore diff configs during sync (#8078)
- feat: Provide address flag for admin dashboard command (#8095)
- feat: Store "Group Nodes" button state in application details preferences (#8036)
- feat: Support specifying cluster by name in addition to API server URL in Cluster API (#8077)
- feat: Support XDG Base directory standard (#7638) (#7791)
- feat: Use encrypted cookie to store OAuth2 state nonce (instead of redis) (#8241)
- feat: Build images on PR and conditionally build arm64 image on push (#8108)

### Bug Fixes

- fix: Add "Restarting MinIO" status to MiniO Tenant health check (#8191)
- fix: Add all resources in list view (#7295)
- fix: Adding pagination to grouped nodes sliding panel#7837 (#7915)
- fix: Allow all resources to add external links (#7923)
- fix: Always call ValidateDestination (#7976)
- fix: Application exist panic when execute api call (#8188)
- fix: Application-icons-alignment (#8054)
- fix: Controller panics if resource manifest has incorrect annotation (#8022)
- fix: Correctly handle project field during partial cluster update (#7994)
- fix: Default value for retry validation #8055 (#8064)
- fix: Fix a possible crash when parsing RBAC (#8165)
- fix: Grouped node list missing resources on Compact resources view #8014 (#8018)
- fix: Issue with headless installation (#7958)
- fix: Issue with project scoped resources (#8048)
- fix: Kubernetes labels normalization for Prometheus  (#7925)
- fix: Nested Refresh dropdown does not work on Application Details page #1524 (#7950)
- fix: Network line colors and menu icon alignment (#8059)
- fix: Opening app details shows UI error on some apps (#8016) (#8019)
- fix: Parse to correct uint32 type (#8177)
- fix: Prevent possible nil-pointer deref in normalizer (#8185)
- fix: Prevent possible out-of-bounds access when loading policies (#8186)
- fix: Provide a semantic version parsed version for KUBE_VERSION (#8250)
- fix: Refreshing label toast (#7979)
- fix: Resource details page crashes when resource is not deployed and hide managed fields is selected (#7971)
- fix: Retry disabled text (#8004)
- fix: Route health check stuck in 'Progressing' (#8170)
- fix: Sync window panel is crashed if resource name not contain letters (#8053)
- fix: Targetervision compatible without prefix refs/heads or refs/tags (#7939)
- fix: Trailing line in Filter Dropdown Menus #7821 (#8001)
- fix: Webhook URL matching edge cases (#7981)
- fix(ui): Use consistent case for diff modes (#7945)
- fix: Use gRPC timeout for sidecar CMPs (#8131) (#8236)

### Other

- chore: Bump go-jsonnet to v0.18.0 (#8011)
- chore: Escape proj in regex (#7985)
- chore: Exclude argocd-server rbac for core-install (#8234)
- chore: Log out the resource triggering reconciliation (#8192)
- chore: Migrate to use golang-jwt/jwt v4.2.0 (#8136)
- chore: Move resolveRevision from api-server to repo-server (#7966)
- chore: Update notifications version (#8267)
- chore: Update slack version (#8299)
- chore: Update to Redis 6.2.4 (#8157)
- chore: Upgrade awscli to 2.4.6 and remove python deps (#7947)
- chore: Upgrade base image to ubuntu:21.10 (#8230)
- chore: Upgrade dex to v2.30.2 (https://github.com/dexidp/dex/issues/2326) (#8237)
- chore: Upgrade gitops engine (#8288)
- chore: Upgrade golang to 1.17.6 (#8229)
- chore: Upgrade helm to most recent version (v3.7.2) (#8226)
- chore: Upgrade k8s client to v1.23 (#8213)
- chore: Upgrade kustomize to most recent version (v4.4.1) (#8227)
- refactor: Introduce 'byClusterName' secret index to speedup cluster server URL lookup (#8133)
- refactor: Move project filtering to server side (#8102)

## v2.2.12 (2022-07-29)

### Notes

This is mainly a security related release and updates compatibility with Kubernetes 1.24.

**Attention:** The base image for 2.2.x reached end-of-life on January 20, 2022. This release upgraded the base image to Ubuntu 22.04 LTS. The change should have no effect on the majority of users. But if any of your git providers only supports now-deprecated key hash algorithms, then Application syncing might break. See the [2.1-to-2.2 upgrade notes](https://argo-cd.readthedocs.io/en/latest/operator-manual/upgrading/2.1-2.2/#support-for-private-repo-ssh-keys-using-the-sha-1-signature-hash-algorithm-is-removed-in-2212) for details and workaround instructions.

### Bug fixes

- fix: create serviceaccount token for v1.24 clusters (#9546)
- fix: upgrade moment from 2.29.2 to 2.29.3 (#9330)
- fix: avoid CVE-2022-28948 (#10093)

### Other changes

- chore: Remove deprecated K8s versions from test matrix
- chore: Go mod tidy
- test: Remove circular symlinks from testdata (#9886)
- test: Fix e2e tests for release-2.2 branch
- chore: bump redoc vesion to avoid CVE-2021-23820 (#8604)
- chore(deps): bump moment from 2.29.3 to 2.29.4 in /ui (#9897)
- chore: upgrade moment to latest version to fix CVE (#9005)
- chore: move dependencies to dev dependencies (#8541)
- docs: add OpenSSH breaking change notes (#10104)
- chore: update parse-url (#10101)
- chore: fix codegen
- chore: fix codegen
- chore: upgrade base image to 22.04 (#10105)
- docs: simplify Docker toolchain docs (#9966) (#10006)
- chore: update redis to 6.2.7 avoid CVE-2022-30065/CVE-2022-2097 (#10068)
- chore: upgrade Dex to 2.32.0 (#10036) (#10042)
- chore: update haproxy to 2.0.29 for redis-ha (#10045)
- test: check for error messages from CI env (#9953)

## v2.2.11 (2022-07-12)

### Security fixes

* HIGH: Certificate verification is skipped for connections to OIDC providers ([GHSA-7943-82jg-wmw5](https://github.com/argoproj/argo-cd/security/advisories/GHSA-7943-82jg-wmw5))
* LOW: A leaked API server encryption key can allow XSS for SSO users ([GHSA-pmjg-52h9-72qv](https://github.com/argoproj/argo-cd/security/advisories/GHSA-pmjg-52h9-72qv))

### Potentially-breaking changes

The fix for GHSA-7943-82jg-wmw5 enables TLS certificate validation by default for connections to OIDC providers. If
connections to your OIDC provider fails validation, SSO will be broken for your Argo CD instance. You should test 2.2.11
before upgrading it to production. From the new documentation:

> By default, all connections made by the API server to OIDC providers (either external providers or the bundled Dex
> instance) must pass certificate validation. These connections occur when getting the OIDC provider's well-known
> configuration, when getting the OIDC provider's keys, and  when exchanging an authorization code or verifying an ID
> token as part of an OIDC login flow.
>
> Disabling certificate verification might make sense if:
> * You are using the bundled Dex instance **and** your Argo CD instance has TLS configured with a self-signed certificate
    >   **and** you understand and accept the risks of skipping OIDC provider cert verification.
> * You are using an external OIDC provider **and** that provider uses an invalid certificate **and** you cannot solve
    >   the problem by setting `oidcConfig.rootCA` **and** you understand and accept the risks of skipping OIDC provider cert
    >   verification.
>
> If either of those two applies, then you can disable OIDC provider certificate verification by setting
> `oidc.tls.insecure.skip.verify` to `"true"` in the `argocd-cm` ConfigMap.

### Features

* feat: enable specifying root ca for oidc (#6712)

### Bug fixes

* fix: webhook typo in case of error in GetManifests (#9671)

## v2.2.10 (2022-06-21)

### Security fixes

* CRITICAL: External URLs for Deployments can include javascript ([GHSA-h4w9-6x78-8vrj](https://github.com/argoproj/argo-cd/security/advisories/GHSA-h4w9-6x78-8vrj))
* HIGH: Insecure entropy in PKCE/Oauth2/OIDC params ([GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v))
* MODERATE: DoS through large directory app manifest files ([GHSA-jhqp-vf4w-rpwq](https://github.com/argoproj/argo-cd/security/advisories/GHSA-jhqp-vf4w-rpwq))
* MODERATE: Symlink following allows leaking out-of-bounds YAML files from Argo CD repo-server ([GHSA-q4w5-4gq2-98vm](https://github.com/argoproj/argo-cd/security/advisories/GHSA-q4w5-4gq2-98vm))

### Potentially-breaking changes

From the [GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v) description:

> The patch introduces a new `reposerver.max.combined.directory.manifests.size` config parameter, which you should tune before upgrading in production. It caps the maximum total file size of .yaml/.yml/.json files in directory-type (raw manifest) Applications. The default max is 10M per Application. This max is designed to keep any single app from consuming more than 3G of memory in the repo-server (manifests consume more space in memory than on disk). The 300x ratio assumes a maliciously-crafted manifest file. If you only want to protect against accidental excessive memory use, it is probably safe to use a smaller ratio.
>
> If your organization uses directory-type Applications with very many manifests or very large manifests then check the size of those manifests and tune the config parameter before deploying this change to production. When testing, make sure to do a "hard refresh" in either the CLI or UI to test your directory-type App. That will make sure you're using the new max logic instead of relying on cached manifest responses from Redis.

### Bug fixes

* fix: missing Helm params (#9565) (#9566)

### Other

* test: directory app manifest generation (#9503)
* test: fix erroneous test change
* chore: eliminate go-mpatch dependency (#9045)
* chore: Make unit tests run on platforms other than amd64 (#8995)
* chore: remove obsolete repo-server unit test (#9559)
* chore: upgrade golangci-lint to v1.46.2 (#9448)
* chore: update golangci-lint (#8988)

## v2.2.9 (2022-05-18)

### Notes

This is a security release. We urge all users of the 2.2.z branch to update as soon as possible. Please refer to the _Security fixes_ section below for more details.

### Security fixes

- CRITICAL: Argo CD will trust invalid JWT claims if anonymous access is enabled (https://github.com/argoproj/argo-cd/security/advisories/GHSA-r642-gv9p-2wjj)
- LOW: Login screen allows message spoofing if SSO is enabled (https://github.com/argoproj/argo-cd/security/advisories/GHSA-xmg8-99r8-jc2j)
- MODERATE: Symlink following allows leaking out-of-bound manifests and JSON files from Argo CD repo-server (https://github.com/argoproj/argo-cd/security/advisories/GHSA-6gcg-hp2x-q54h)

## v2.2.8 (2022-03-22)

### Special notes

This release contains the fix for a security issue with critical severity. We recommend users on the 2.2 release branch to update to this release as soon as possible.

More information can be found in the related
[security advisory](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2f5v-8r3f-8pww).

### Changes

As part of the security fix, the Argo CD UI no longer automatically presents child resources of allow-listed resources unless the child resources are also allow-listed. For example, Pods are not going to show up if only Deployment is added to the allow-list.

If you have [projects](https://argo-cd.readthedocs.io/en/stable/user-guide/projects/) configured with allow-lists, make sure the allow-lists include all the resources you want users to be able to view/manage through the UI. For example, if your project allows `Deployments`, you would add `ReplicaSets` and `Pods`.

#### Bug Fixes

- fix: application resource APIs must enforce project restrictions

## v2.2.7 (2022-03-08)

### Bug Fixes

- fix: correct jsonnet paths resolution (#8721)

## v2.2.6 (2022-03-06)

### Bug Fixes

- fix: prevent file traversal using helm file values param and application details api (#8606)
- fix!: enforce app create/update privileges when getting repo details (#8558)
- feat: support custom helm values file schemes (#8535)

## v2.2.5 (2022-02-04)

- fix: Resolve symlinked value files correctly (#8387)

## v2.2.4 (2022-02-03)

### Special notes

This release contains the fix for a security issue with high severity. We recommend users on the 2.2 release branch to update to this release as soon as possible.

More information can be found in the related
[security advisory](https://github.com/argoproj/argo-cd/security/advisories/GHSA-63qx-x74g-jcr7)

### Bug Fixes

- fix: Prevent value files outside repository root

### Other changes

- chore: upgrade dex to v2.30.2 (backport of #8237) (#8257)

## v2.2.3 (2022-01-18)

- fix: Application exist panic when execute api call (#8188)
- fix: Route health check stuck in 'Progressing' (#8170)
- refactor: Introduce 'byClusterName' secret index to speedup cluster server URL lookup (#8133)
- chore: Update to Redis 6.2.4 (#8157) (#8158)

## v2.2.2 (2021-12-31)

- fix: Issue with project scoped resources (#8048)
- fix: Escape proj in regex (#7985)
- fix: Default value for retry validation #8055 (#8064)
- fix: Sync window panel is crashed if resource name not contain letters (#8053)
- fix: Upgrade github.com/argoproj/gitops-engine to v0.5.2
- fix: Retry disabled text (#8004)
- fix: Opening app details shows UI error on some apps (#8016) (#8019)
- fix: Correctly handle project field during partial cluster update (#7994)
- fix: Cluster API does not support updating labels and annotations (#7901)

## v2.2.1 (2021-12-16)

- fix: Resource details page crashes when resource is not deployed and hide managed fields is selected (#7971)
- fix: Issue with headless installation (#7958)
- fix: Nil pointer (#7905)

## v2.2.0 (2021-12-14)

> [Upgrade instructions](./docs/operator-manual/upgrading/2.1-2.2.md)

### Project Scoped repositories and clusters

The project scoped repositories and clusters is a feature that simplifies registering the repositories and cluster credentials.
Instead of requiring operators to set up in advance all clusters and git repositories that can be used, developers can now do
this on their own in a self-service manner.

### Config Management Plugins V2

The Config Management Plugins V2 is set of enhancement of the existing config management plugins feature.
The list includes improved installation experience, ability to package plugin into a separate image and
improved plugin manifests discovery.

### Resource tracking

Argo CD has traditionally tracked the resources it manages by the well-known "app.kubernetes.io/instance" property.
While using this property works ok in simple scenarios, it also has several limitations. ArgoCD now allows you to use
a new annotation (argocd.argoproj.io/tracking-id) for tracking your resources. Using this annotation is a much more flexible approach
as there are no conflicts with other Kubernetes tools, and you can easily install multiple Argo CD instances on the same clusters.

### Bug Fixes and Performance Enhancements

* Argo CD API server caches RBAC checks that significantly improves the GET /api/v1/applications API performance (#7587)
* Argo CD RBAC supports regex matches (#7165)
* Health check support for KubeVirt (#7176), Cassandra (#7017), Openshift Route (#7112), DeploymentConfig (#7114), Confluent (#6957) and SparkApplication (#7434) CRDs.
* Persistent banner (#7312) with custom positioning (#7462)
* Cluster name support in project destinations (#7198)
* around 30 more features and a total of 84 bug fixes

## v2.1.16 (2022-06-21)

### Security fixes

* CRITICAL: External URLs for Deployments can include javascript ([GHSA-h4w9-6x78-8vrj](https://github.com/argoproj/argo-cd/security/advisories/GHSA-h4w9-6x78-8vrj))
* HIGH: Insecure entropy in PKCE/Oauth2/OIDC params ([GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v))
* MODERATE: DoS through large directory app manifest files ([GHSA-jhqp-vf4w-rpwq](https://github.com/argoproj/argo-cd/security/advisories/GHSA-jhqp-vf4w-rpwq))
* MODERATE: Symlink following allows leaking out-of-bounds YAML files from Argo CD repo-server ([GHSA-q4w5-4gq2-98vm](https://github.com/argoproj/argo-cd/security/advisories/GHSA-q4w5-4gq2-98vm))

**Note:** This will be the last security fix release in the 2.1.x series. Please [upgrade to a newer minor version](https://argo-cd.readthedocs.io/en/latest/operator-manual/upgrading/overview/) to continue to get security fixes.

### Potentially-breaking changes

From the [GHSA-2m7h-86qq-fp4v](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2m7h-86qq-fp4v) description:

> The patch introduces a new `reposerver.max.combined.directory.manifests.size` config parameter, which you should tune before upgrading in production. It caps the maximum total file size of .yaml/.yml/.json files in directory-type (raw manifest) Applications. The default max is 10M per Application. This max is designed to keep any single app from consuming more than 3G of memory in the repo-server (manifests consume more space in memory than on disk). The 300x ratio assumes a maliciously-crafted manifest file. If you only want to protect against accidental excessive memory use, it is probably safe to use a smaller ratio.
>
> If your organization uses directory-type Applications with very many manifests or very large manifests then check the size of those manifests and tune the config parameter before deploying this change to production. When testing, make sure to do a "hard refresh" in either the CLI or UI to test your directory-type App. That will make sure you're using the new max logic instead of relying on cached manifest responses from Redis.

### Bug fixes

* fix: missing Helm params (#9565) (#9566)

### Other

* test: directory app manifest generation (#9503)
* test: fix erroneous test change
* chore: eliminate go-mpatch dependency (#9045)
* chore: Make unit tests run on platforms other than amd64 (#8995)
* chore: remove obsolete repo-server unit test (#9559)
* chore: upgrade golangci-lint to v1.46.2 (#9448)
* chore: update golangci-lint (#8988)
* test: fix ErrorContains (#9445)

## v2.1.15 (2022-05-18)

### Notes

This is a security release. We urge all users of the 2.1.z branch to update as soon as possible. Please refer to the _Security fixes_ section below for more details.

### Security fixes

- CRITICAL: Argo CD will trust invalid JWT claims if anonymous access is enabled (https://github.com/argoproj/argo-cd/security/advisories/GHSA-r642-gv9p-2wjj)
- LOW: Login screen allows message spoofing if SSO is enabled (https://github.com/argoproj/argo-cd/security/advisories/GHSA-xmg8-99r8-jc2j)
- MODERATE: Symlink following allows leaking out-of-bound manifests and JSON files from Argo CD repo-server (https://github.com/argoproj/argo-cd/security/advisories/GHSA-6gcg-hp2x-q54h)

## v2.1.14 (2022-03-22)

### Special notes

This release contains the fix for a security issue with critical severity. We recommend users on the 2.1 release branch to update to this release as soon as possible.

More information can be found in the related
[security advisory](https://github.com/argoproj/argo-cd/security/advisories/GHSA-2f5v-8r3f-8pww).

### Changes

As part of the security fix, the Argo CD UI no longer automatically presents child resources of allow-listed resources unless the child resources are also allow-listed. For example, Pods are not going to show up if only Deployment is added to the allow-list.

If you have [projects](https://argo-cd.readthedocs.io/en/stable/user-guide/projects/) configured with allow-lists, make sure the allow-lists include all the resources you want users to be able to view/manage through the UI. For example, if your project allows `Deployments`, you would add `ReplicaSets` and `Pods`.

#### Bug Fixes

- fix: application resource APIs must enforce project restrictions

## v2.1.13 (2022-03-22)

Unused release number.

## v2.1.12 (2022-03-08)

### Bug Fixes

- fix: correct jsonnet paths resolution (#8721)

## v2.1.11 (2022-03-06)

### Bug Fixes

- fix: prevent file traversal using helm file values param and application details api (#8606)
- fix!: enforce app create/update privileges when getting repo details (#8558)
- feat: support custom helm values file schemes (#8535)

## v2.1.10 (2022-02-04)

### Bug Fixes

- fix: Resolve symlinked value files correctly (#8387)

## v2.1.9 (2022-02-03)

### Special notes

This release contains the fix for a security issue with high severity. We recommend users on the 2.1 release branch to update to this release as soon as possible.

More information can be found in the related
[security advisory](https://github.com/argoproj/argo-cd/security/advisories/GHSA-63qx-x74g-jcr7)

### Bug Fixes

- fix: Prevent value files outside repository root

## v2.1.8 (2021-12-13)

### Bug Fixes

- fix: issue with keepalive (#7861)
- fix nil pointer dereference error (#7905)
- fix: env vars to tune cluster cache were broken (#7779)
- fix: upgraded gitops engine to v0.4.2 (fixes #7561)

## v2.1.7 (2021-12-14)

- fix: issue with keepalive (#7861)
- fix nil pointer dereference error (#7905)
- fix: env vars to tune cluster cache were broken (#7779)
- fix: upgraded gitops engine to v0.4.2 (fixes #7561)


## v2.1.6 (2021-11-16)

- fix: don't use revision caching during app creation (#7508)
- fix: supporting OCI dependencies. Fixes #6062 (#6994)

## v2.1.5 (2021-11-16)

- fix: Invalid memory address or nil pointer dereference in processRequestedAppOperation (#7501)

## v2.1.4 (2021-11-15)

- fix: Operation has completed with phase: Running (#7482)
- fix: Application status panel shows Syncing instead of Deleting (#7486)
- fix(ui): Add Error Boundary around Extensions and comply with new Extensions API (#7215)


## v2.1.3 (2021-10-29)

- fix: core-install.yaml always refers to latest argocd image (#7321)
- fix: handle applicationset backup forbidden error (#7306)
- fix: Argo CD should not use cached git/helm revision during app creation/update validation (#7244)

## v2.1.2 (2021-10-02)

- fix: cluster filter popping out of box (#7135)
- fix: gracefully shutdown metrics server when dex config changes (#7138)
- fix: upgrade gitops engine version to v0.4.1 (#7088)
- fix: repository name already exists when multiple helm dependencies  (#7096)


## v2.1.1 (2021-08-25)

### Bug Fixes

- fix: password reset requirements (#7071)
- fix: Custom Styles feature is broken (#7067)
- fix(ui): Add State to props passed to Extensions (#7045)
- fix: keep uid_entrypoint.sh for backward compatibility (#7047)

## v2.1.0 (2021-08-20)

> [Upgrade instructions](./docs/operator-manual/upgrading/2.0-2.1.md)

### Argo CD Core

Argo CD Core - lightweight Argo CD distribution that packages only core GitOps features and relies
on Kubernetes API/RBAC to power UI and CLI.

### Core Features

* The synchronization process became much much faster and requires significantly less memory.
* An additional caching that ensures that each repository's target revisions are queried only once per
  reconciliation cycle. This dramatically reduces the number of Git requests.
* Improved Diffing Customizations: use JQ path expressions to exclude required fields from the diffing.
* Health assessment support for new CRDs: introduced health assessment of CRDs from trident.netapp.io,
  elasticsearch.k8s.elastic.co, cluster.x-k8s.io, and minio.min.io API groups.

### Improved Settings

A set of changes had been implemented to simplify configuring Argo CD.

* Simplified Repository Registration: you no longer need to modify the argocd-cm ConfigMap to register a
  new Git or Helm repository.
* Enhanced Resource Customizations: the resource.customizations key has been deprecated in favor of
  a separate ConfigMap key per resource.
* Reference secret values from any Kubernetes secret: starting v2.1 you can use sensitive data stored in 
  any Kubernetes secret to configure Argo CD.
* Simplify parametrization of Argo CD server processes: an additional optional ConfigMap argocd-cmd-params-cm
  has been introduced.

### Refreshed User Interface

* Enhanced and more consistent filters on Applications List and Applications Details pages.
* Status bar on the Application List page.
* The redesigned search box on the Application List page and more.

### The argocd-util CLI deprecation

The argocd CLI and now available under argocd admin subcommand.

## v2.0.5 (2021-07-22)

* fix: allow argocd-notification ingress to repo-server (#6746)
* fix: argocd-server crashes due to nil pointer dereference (#6757)
* fix: WebUI failure when loading pod view 't.parentRefs is undefined' (#6490) (#6535)
* fix: prevent 'cannot read property "filter" of undefined' during nodes filtering (#6453)
* fix: download Pod Logs button not honouring argocd-server rootpath (#6548) (#6627)
* fix: Version warning banner in docs (#6682)
* fix: upgrade gitops engine to fix workflow health check

## v2.0.4 (2021-06-22)

* fix: typo in networkPolicy definition in manifests (#6532)
* fix: Update redis to 6.2.4 (#6475)
* fix: allows access to dex metrics from any pod (#6420)
* fix: add client side retry to prevent 'transport is closing' errors (#6402)
* fix: Update documentation Argocd app CRD health with app of apps (#6281)
* fix(ui): Crash on application pod view (#6384)
* chore: pin mkdocs version to fix docs build (#6421)
* chore: regenerate manifests using codegen (#6422)
* refactor: use RLock and RUnlock for project to improve performance (#6225)
* chore: Update Golang to v1.16.4 (#6358)

## v2.0.3 (2021-05-27)

### Bug Fixes

* fix: add missing --container flag to 'argocd app logs' command (#6320)
* fix: grpc web proxy must ensure to read full header (#6319)
* fix: controller should refresh app before running sync operation (#6294)

## v2.0.2 (2021-05-20)

### Bug Fixes

* fix: enable access to metrics port in embedded network policies (#6277)
* fix: display log streaming error in logs viewer (#6100) (#6273)
* fix: Don't count errored or completed neighbor pods toward resource consumption (#6259)
* fix: Enable kex algo diffie-hellman-group-exchange-sha256 for go-git ssh (#6256)
* fix: copy github app key from repocreds (#6140, #6197)
* fix(ui): UI crashes after reinstalling ArgoCD (#6218)
* fix: add network policies to restrict traffic flow between argocd components (#6156)
* fix: Revert "feat: Add health checks for kubernetes-external-secrets (#5435)"
* chore: Allow ingress traffic to argocd-server by default (#6179)

## v2.0.1 (2021-04-15)

### Bug Fixes

* fix: spark application check fails on missing section (#6036)
* fix: Adding explicit bind to redis and sentinel for IPv4 clusters #5957 (#6005)
* fix: fix: use correct field for evaluating whether or not GitHub Enterprise is selected (#5987)

## v2.0.0 (2021-04-07)

> [Upgrade instructions](./docs/operator-manual/upgrading/1.8-2.0.md)

### Pods View

Pods View is particularly useful for applications that have hundreds of pods. Instead of visualizing all Kubernetes
resources for the application, it only shows Kubernetes pods and closely related resources. The Pods View supports
grouping related resources by Parent Resource, Top Level Parent, or by Node. Each way of grouping solves a particular
use case. For example grouping by Top Level Parent allows you to quickly find how many pods your application is running
and which resources created them. Grouping by Node allows to see how Pods are spread across the nodes and how many
resources they requested.


### Logs Viewer

Argo CD provides a way to see live logs of pods, which is very useful for debugging and troubleshooting. In the v2.0
release, the log visualization has been rewritten to support pagination, filtering, the ability to disable/enable log
streaming, and even a dark mode for terminal lovers. Do you want to see aggregated logs of multiple deployment pods?
Not a problem! Just click on the parent resource such as Deployment, ReplicaSet, or StatefulSet and navigate
to the Logs tab.

### Banner Feature

Want to notify your Argo CD users of upcoming changes? Just specify the notification message and optional URL using the
`ui.bannercontent` and `ui.bannerurl` attributes in the `argocd-cm` ConfigMap. 

### Core Features

* The new sync option `PrunePropagationPolicy=background` allows using background deletion during syncing
* New application finalizer `resources-finalizer.argocd.argoproj.io:background` allows using background deletion when the application is deleted
* The new sync option `ApplyOutOfSyncOnly=true` allows skipping syncing resources that are already in the desired state.
* The new sync option `PruneLast=true` allows deferring resource pruning until the last synchronization phase after all other resources are synced and healthy.

### The argocd-util CLI

Argo CD Util is a CLI tool that contains useful commands for operators who manage Argo CD. Starting from this release
the Argo CD Utility is published with every Argo CD release as a Homebrew installation.

## v1.8.7 (2021-02-26)

### Important note
This release fixed a regression regarding which cluster resources are permitted on the AppProject level.
Previous to this fix, after #3960 has been merged, all cluster resources were allowed on project level when neither of
the allow or deny lists was defined. However, the correct behavior is to block all resources in this case.

If you have Projects with empty allow and deny lists, but want the associated applications be able to sync cluster
resources, you will have to adapt your cluster resources allow lists to explicitly allow the resources.

- fix: redact sensitive data in logs (#5662)
- fix: Properly escape HTML for error message from CLI SSO (#5563)
- fix: Empty resource whitelist allowed all resources (#5540) (#5551)

## v1.8.6 (2021-02-26)

- fix: Properly escape HTML for error message from CLI SSO (#5563)
- fix: API server should not print resource body when resource update fails (#5617)
- fix: fix memory leak in application controller (#5604)

## v1.8.5 (2021-02-19)

- fix: 'argocd app wait --suspended' stuck if operation is in progress (#5511)
- fix: Presync hooks stop working after namespace resource is added in a Helm chart #5522
- docs: add the missing rbac resources to the documentation (#5476)
- refactor: optimize argocd-application-controller redis usage (#5345)

## v1.8.4 (2021-02-05)

- feat: set X-XSS-Protection while serving static content (#5412)
- fix: version info should be available if anonymous access is enabled (#5422)
- fix: disable jwt claim audience validation #5381 (#5413)
- fix: /api/version should not return tools version for unauthenticated requests (#5415)
- fix: account tokens should be rejected if required capability is disabled (#5414)
- fix: tokens keep working after account is deactivated (#5402)
- fix: a request which was using a revoked project token, would still be allowed to perform requests allowed by default policy (#5378)

## v1.8.3 (2021-01-21)

- fix: make sure JWT token time fields contain only integer values (#5228)

## v1.8.2 (2021-01-09)

### Bug Fixes

- fix: updating cluster drops secret (#5220)
- fix: remove invalid assumption about OCI helm chart path (#5179)
- fix: Possible nil pointer dereference in repository API (#5128)
- fix: Possible nil pointer dereference in repocreds API (#5130)
- fix: use json serialization to store cache instead of github.com/vmihailenco/msgpack (#4965)
- fix: add liveness probe to restart repo server if it fails to server tls requests (#5110) (#5119)
- fix: Allow correct SSO redirect URL for CLI static client (#5098)
- fix: add grpc health check (#5060)
- fix: setting 'revision history limit' errors in UI (#5035)
- fix: add api-server liveness probe that catches bad data in informer (#5026)

### Refactoring

- chore: Update Dex to v2.27.0 (#5058)
- chore: Upgrade gorilla/handlers and gorilla/websocket (#5186)
- chore: Upgrade jwt-go to 4.0.0-preview1 (#5184)

## v1.8.1 (2020-12-09)

- fix: sync retry is broken for multi-phase syncs (#5017)

## v1.8.0 (2020-12-09)

### Mono-Repository Improvements

Enhanced performance during manifest generation from mono-repository - the repository that represents the
desired state of the whole cluster and contains hundreds of applications. The improved argocd-repo-server
now able to concurrently generate manifests from the same repository and for the same commit SHA. This
might provide 10x performance improvement of manifests generation.

### Annotation Based Path Detection

The feature that allows specifying which source repository directories influence the application manifest generation
using the `argocd.argoproj.io/manifest-generate-paths` annotation. The annotation improves the Git webhook handler
behavior. The webhook avoids related applications reconciliation if no related files have been changed by the Git commit
and even allows to skip manifests generation for new commit by re-using generation manifests for the previous commit.

### Horizontal Controller Scaling

This release allows scaling the `argocd-application-controller` horizontally. This allows you to manage as many Kubernetes clusters
as needed using a single Argo CD instance.

## New Core Functionality Features

Besides performance improvements, Argo CD got a lot of usability enhancements and new features:

* Namespace and CRD creation [#4354](https://github.com/argoproj/argo-cd/issues/4354)
* Unknown fields of built-in K8S types [#1787](https://github.com/argoproj/argo-cd/issues/1787)
* Endpoints Diffing [#1816](https://github.com/argoproj/argo-cd/issues/1816)
* Better compatibility with Helm Hooks [#1816](https://github.com/argoproj/argo-cd/issues/1816)
* App-of-Apps Health Assessment [#3781](https://github.com/argoproj/argo-cd/issues/3781)

## Global Projects

This release makes it easy to manage an Argo CD that has hundreds of Projects. Instead of duplicating the same organization-wide rules in all projects
you can put such rules into one project and make this project “global” for all other projects. Rules defined in the global project are inherited by all
other projects and therefore don’t have to be duplicated. The sample below demonstrates how you can create a global project and specify which project should
inherit global project rules using Kubernetes labels. 

## User Interface Improvements

The Argo CD user interface is an important part of a project and we keep working hard on improving the user experience. Here is an incomplete list of implemented improvements:

* Improved Applications Filters [#4622](https://github.com/argoproj/argo-cd/issues/4622)
* Git tags and branches autocompletion [#4713](https://github.com/argoproj/argo-cd/issues/4713)
* Project Details Page [#4400](https://github.com/argoproj/argo-cd/issues/4400)
* New version information panel [#4376](https://github.com/argoproj/argo-cd/issues/4376)
* Progress Indicators [#4411](https://github.com/argoproj/argo-cd/issues/4411)
* External links annotations [#4380](https://github.com/argoproj/argo-cd/issues/4380) and more!

## Config Management Tools Enhancements

* OCI Based Repositories [#4018](https://github.com/argoproj/argo-cd/issues/4018)
* Configurable Helm Versions [#4111](https://github.com/argoproj/argo-cd/issues/4111)

## Bug fixes and under the hood changes

In addition to new features and enhancements, we’ve fixed more than 50 bugs and upgraded third-party components and libraries that Argo CD relies on.

## v1.7.9 (2020-11-17)

- fix: improve commit verification tolerance (#4825)
- fix: argocd diff --local should not print data of local secrets (#4850)
- fix(ui): stack overflow crash of resource tree view for large applications (#4685)
- chore: Update golang to v1.14.12 [backport to release-1.7] (#4834)
- chore: Update redis to 5.0.10 (#4767)
- chore: Replace deprecated GH actions directives for integration tests (#4589)

## v1.7.8 (2020-10-15)

- fix(logging.go): changing marshaler for JSON logging to use gogo (#4319)
- fix: login with apiKey capability (#4557)
- fix: api-server should not try creating default project it is exists already (#4517)
- fix: JS error on application list page if app has no namespace (#4499)


## v1.7.7 (2020-09-28)

- fix: Support transition from a git managed namespace to auto create (#4401)
- fix: reduce memory spikes during cluster cache refresh (#4298)
- fix: No error/warning condition if application destination namespace not monitored by Argo CD (#4329)
- fix: Fix local diff/sync of apps using cluster name (#4201)

## v1.7.6 (2020-09-18)

- fix: Added cluster authentication to AKS clusters (#4265)
- fix: swagger UI stuck loading (#4377)
- fix: prevent 'argocd app sync' hangs if sync is completed too quickly (#4373)
- fix: argocd app wait/sync might stuck (#4350)
- fix: failed syncs are not retried soon enough (#4353)

## v1.7.5 (2020-09-15)

- fix: app create with -f should not ignore other options (#4322)
- fix: limit concurrent list requests across all clusters (#4328)
- fix: fix possible deadlock in /v1/api/stream/applications and /v1/api/application APIs (#4315)
- fix: WatchResourceTree does not enforce RBAC (#4311)
- fix: app refresh API should use app resource version (#4303)
- fix: use informer instead of k8s watch to ensure app is refreshed (#4290)


## v1.7.4 (2020-09-04)

- fix: automatically stop watch API requests when page is hidden (#4269)
- fix: upgrade gitops-engine dependency (issues #4242, #1881) (#4268)
- fix: application stream API should not return 'ADDED' events if resource version is provided (#4260)
- fix: return parsing error (#3942)
- fix: JS error when using cluster filter in the /application view (#4247)
- fix: improve applications list page client side performance (#4244)

## v1.7.3 (2020-09-01)

- fix: application details page crash when app is deleted (#4229)
- fix: api-server unnecessary normalize projects on every start (#4219)
- fix: load only project names in UI (#4217)
- fix: Re-create already initialized ARGOCD_GNUPGHOME on startup (#4214) (#4223)
- fix: Add openshift as a dex connector type which requires a redirectURI (#4222)
- fix: Replace status.observedAt with redis pub/sub channels for resource tree updates (#1340) (#4208)
- fix: cache inconsistency of child resources (#4053) (#4202)
- fix: do not include kube-api check in application liveness flow (#4163)

## v1.7.2 (2020-08-27)

- fix: Sync hangs with cert-manager on latest RC (#4105)
- fix: support for PKCE for cli login (#2932)

## v1.7.2 (2020-08-25)

- fix: Unable to create project JWT token on K8S v1.15 (#4165)
- fix: Argo CD does not exclude creationTimestamp from diffing (#4157)

## v1.7.0 (2020-08-24)

### GnuPG Signature Verification

The feature allows to only sync against commits that are signed in Git using GnuPG. The list of public 
GPG keys required for verification is configured at the system level and can be managed using Argo CD CLI or Web user interface.
The keys management is integrated with Argo CD SSO and access control system (e.g. `argocd gpg add --from <path-to-key>`)

The signature verification is enabled on the project level. The ApplicationProject CRD has a new signatureKeys field that includes
a list of imported public GPG keys. Argo CD will verify the commit signature by these keys for every project application.

### Cluster Management Enhancements

The feature allows using the cluster name instead of the URL to specify the application destination cluster.
Additionally, the cluster CLI and Web user interface have been improved. Argo CD operators now can view and edit cluster
details using the Cluster Details page. The page includes cluster settings details as well as runtime information such
as the number of monitored Kubernetes resources.

### Diffing And Synchronization Usability

* **Diffing logic improvement** Argo CD performs client-side resource diffing to detect deviations and present detected
differences in the UI and CLI. The 1.7 release aligns a comparison algorithm with server-side Kubernetes implementation
and removes inaccuracies in some edge cases.

* **Helm Hooks Compatibility** The improvement removes the discrepancy between the way how Argo CD and Helm deletes
hooks resources. This significantly improves the compatibility and enables additional use cases.

* **Namespace Auto-Creation** With a new option for applications Argo CD will ensure that namespace specified as the
application destination exists in the destination cluster. 

* **Failed Sync Retry** This feature enables retrying of failed synchronization attempts during both manually-triggered
and automated synchronization.

### Orphaned Resources Monitoring Enhancement

The enhancement allows configuring an exception list in Orphaned Resources settings to avoid false alarms.

## v1.6.2 (2020-08-01)

- feat: adding validate for app create and app set (#4016)
- fix: use glob matcher in casbin built-in model (#3966)
- fix: Normalize Helm chart path when chart name contains a slash (#3987)
- fix: allow duplicates when using generateName (#3878)
- fix: nil pointer dereference while syncing an app (#3915)

## v1.6.1 (2020-06-18)

- fix: User unable to generate project token even if account has appropriate permissions (#3804)

## v1.6.0 (2020-06-16)

[1.6 Release blog post](https://blog.argoproj.io/argo-cd-v1-6-democratizing-gitops-with-gitops-engine-5a17cfc87d62)

### GitOps Engine

As part of 1.6 release, the core Argo CD functionality has been moved into [GitOps Engine](https://github.com/argoproj/gitops-engine).
GitOps Engine is a reusable library that empowers you to quickly build specialized tools that implement specific GitOps
use cases, such as bootstrapping a Kubernetes cluster, or decentralized management of namespaces.

#### Enhancements

- feat: upgrade kustomize to v3.6.1 version (#3696)
- feat: Add build support for ARM images (#3554)
- feat: CLI: Allow setting Helm values literal (#3601) (#3646)
- feat: argocd-util settings resource-overrides list-actions (#3616)
- feat: adding failure retry (#3548)
- feat: Implement GKE ManagedCertificate CRD health checks (#3600)
- feat: Introduce diff normalizer knobs and allow for ignoring aggregated cluster roles (#2382) (#3076)
- feat: Implement Crossplane CRD health checks (#3581)
- feat: Adding deploy time and duration label (#3563)
- feat: support delete cluster from UI (#3555)
- feat: add button loading status for time-consuming operations (#3559)
- feat: Add --logformat switch to API server, repository server and controller (#3408)
- feat: Add a Get Repo command to see if Argo CD has a repo (#3523)
- feat: Allow selecting TLS ciphers on server (#3524)
- feat: Support additional metadata in Application sync operation (#3747)
- feat: upgrade redis to 5.0.8-alpine (#3783)

#### Bug Fixes

- fix: settings manager should invalidate cache after updating repositories/repository credentials (#3672)
- fix: Allow unsetting the last remaining values file (#3644) (#3645)
- fix: Read cert data from kubeconfig during cluster addition and use if present (#3655) (#3667)
- fix: oidc should set samesite cookie (#3632)
- fix: Allow underscores in hostnames in certificate module (#3596)
- fix: apply scopes from argocd-rbac-cm to project jwt group searches (#3508)
- fix: fix nil pointer dereference error after cluster deletion (#3634)
- fix: Prevent possible nil pointer dereference when getting Helm client (#3613)
- fix: Allow CLI version command to succeed without server connection (#3049) (#3550)
- fix: Fix login with port forwarding (#3574)
- fix: use 'git show-ref' to both retrieve and store generated manifests (#3578)
- fix: enable redis retries; add redis request duration metric (#3575)
- fix: Disable keep-alive for HTTPS connection to Git (#3531)
- fix: use uid instead of named user in Dockerfile (#3108)

#### Other

- refactoring: GitOps engine (#3066)

## v1.5.8 (2020-06-16)

- fix: upgrade awscli version (#3774)
- fix: html encode login error/description before rendering it (#3773)
- fix: oidc should set samesite cookie (#3632)
- fix: avoid panic in badge handler (#3741)

## v1.5.7 (2020-06-09)

The 1.5.7 patch release resolves issue #3719 . The ARGOCD_ENABLE_LEGACY_DIFF=true should be added to argocd-application-controller deployment.

- fix: application with EnvoyFilter causes high memory/CPU usage (#3719)

## v1.5.6 (2020-06-02)

- feat: Upgrade kustomize to 3.6.1
- fix: Prevent possible nil pointer dereference when getting Helm client (#3613)
- fix: avoid deadlock in settings manager (#3637)

## v1.5.5 (2020-05-16)

- feat: add Rollout restart action (#3557)
- fix: enable redis retries; add redis request duration metric (#3547)
- fix: when --rootpath is on, 404 is returned when URL contains encoded URI (#3564)

## v1.5.4 (2020-05-05)

- fix: CLI commands with --grpc-web

## v1.5.3 (2020-05-01)

This patch release introduces a set of enhancements and bug fixes. Here are most notable changes:

#### Multiple Kustomize Versions

The bundled Kustomize version had been upgraded to v3.5.4. Argo CD allows changing bundled version using
[custom image or init container](https://argoproj.github.io/argo-cd/operator-manual/custom_tools/). 
This [feature](https://argoproj.github.io/argo-cd/user-guide/kustomize/#custom-kustomize-versions)
enables bundling multiple Kustomize versions at the same time and allows end-users to specify the required version per application.

#### Custom Root Path

The feature allows accessing Argo CD UI and API using a custom root path(for example https://myhostname/argocd).
This enables running Argo CD behind a proxy that takes care of user authentication (such as Ambassador) or hosting
multiple Argo CD using the same hostname. A set of bug fixes and enhancements had been implemented to makes it easier.
Use new `--rootpath` [flag](https://argoproj.github.io/argo-cd/operator-manual/ingress/#argocd-server-and-ui-root-path-v153) to enable the feature.

### Login Rate Limiting

The feature prevents a built-in user password brute force attack and addresses the known 
[vulnerability](https://argoproj.github.io/argo-cd/security_considerations/#cve-2020-8827-insufficient-anti-automationanti-brute-force).

### Settings Management Tools

A new set of [CLI commands](https://argoproj.github.io/argo-cd/operator-manual/troubleshooting/) that simplify configuring Argo CD.
Using the CLI you can test settings changes offline without affecting running Argo CD instance and have ability to troubleshot diffing
customizations, custom resource health checks, and more.

### Other

* New Project and Application CRD settings ([#2900](https://github.com/argoproj/argo-cd/issues/2900), [#2873](https://github.com/argoproj/argo-cd/issues/2873)) that allows customizing Argo CD behavior.
* Upgraded Dex (v2.22.0) enables seamless [SSO integration](https://www.openshift.com/blog/openshift-authentication-integration-with-argocd) with OpenShift.


#### Enhancements

* feat: added --grpc-web-root-path for CLI. (#3483)
* feat: limit the maximum number of concurrent login attempts (#3467)
* feat: upgrade kustomize version to 3.5.4 (#3472)
* feat: upgrade dex to 2.22.0 (#3468)
* feat: support user specified account token ids (#3425)
* feat: support separate Kustomize version per application (#3414)
* feat: add support for dex prometheus metrics (#3249)
* feat: add settings troubleshooting commands to the 'argocd-util' binary (#3398)
* feat: Let user to define meaningful unique JWT token name (#3388)
* feat: Display link between OLM ClusterServiceVersion and it's OperatorGroup (#3390)
* feat: Introduce sync-option SkipDryRunOnMissingResource=true (#2873) (#3247)
* feat: support normalizing CRD fields that use known built-in K8S types (#3357)
* feat: Whitelisted namespace resources (#2900)

#### Bug Fixes

* fix: added path to cookie (#3501)
* fix: 'argocd sync' does not take into account IgnoreExtraneous annotation (#3486)
* fix: CLI renders flipped diff results (#3480)
* fix: GetApplicationSyncWindows API should not validate project permissions (#3456)
* fix: argocd-util kubeconfig should use RawRestConfig to export config (#3447)
* fix: javascript error on accounts list page (#3453)
* fix: support both <group>/<kind> as well as <kind> as a resource override key (#3433)
* fix: Updating to jsonnet v1.15.0 fix issue #3277 (#3431)
* fix for helm repo add with flag --insecure-skip-server-verification (#3420)
* fix: app diff --local support for helm repo. #3151 (#3407)
* fix: Syncing apps incorrectly states "app synced", but this is not true (#3286)
* fix: for jsonnet when it is located in nested subdirectory and uses import (#3372)
* fix: Update 4.5.3 redis-ha helm manifest (#3370)
* fix: return 401 error code if username does not exist (#3369)
* fix: Do not panic while running hooks with short revision (#3368)

## v1.5.2 (2020-04-20)

#### Critical security fix

This release contains a critical security fix. Please refer to the
[security document](https://argoproj.github.io/argo-cd/security_considerations/#CVE-2020-5260-possible-git-credential-leak)
for more information.

**Upgrading is strongly recommended**

## v1.4.3 (2020-04-20)

#### Critical security fix

This release contains a critical security fix. Please refer to the
[security document](https://argoproj.github.io/argo-cd/security_considerations/#CVE-2020-5260-possible-git-credential-leak)
for more information.

## v1.5.1 (2020-04-06)

#### Bug Fixes

* fix: return 401 error code if username does not exist (#3369)
* fix: Do not panic while running hooks with short revision (#3368)
* fix: Increase HAProxy check interval to prevent intermittent failures (#3356)
* fix: Helm v3 CRD are not deployed (#3345)

## v1.5.0 (2020-04-02)

#### Helm Integration Enhancements - Helm 3 Support And More

Introduced native support Helm3 charts. For backward compatibility Helm 2 charts are still rendered using Helm 2 CLI. Argo CD inspects the
Charts.yaml file and choose the right binary based on `apiVersion` value.

Following enhancement were implemented in addition to Helm 3:
* The `--api-version` flag is passed to the `helm template` command during manifest generation.
* The `--set-file` flag can be specified in the application specification.
* Fixed bug that prevents automatically update Helm chart when new version is published (#3193)

#### Better Performance and Improved Metrics

 If you are running Argo CD instances with several hundred applications on it, you should see a
 huge performance boost and significantly less Kubernetes API server load.

 The Argo CD controller Prometheus metrics have been reworked to enable a richer Grafana dashboard.
 The improved dashboard is available at [examples/dashboard.json](https://github.com/argoproj/argo-cd/blob/master/examples/dashboard.json).
 You can set `ARGOCD_LEGACY_CONTROLLER_METRICS=true` environment variable and use [examples/dashboard-legacy.json](https://github.com/argoproj/argo-cd/blob/master/examples/dashboard-legacy.json)
 to keep using old dashboard.

#### Local accounts

The local accounts had been introduced additional to `admin` user and SSO integration. The feature is useful for creating authentication
tokens with limited permissions to automate Argo CD management. Local accounts also could be used small by teams when SSO integration is overkill.
This enhancement also allows to disable admin user and enforce only SSO logins.

#### Redis HA Proxy mode

As part of this release, the bundled Redis was upgraded to version 4.3.4 with enabled HAProxy.
The HA proxy replaced the sentinel and provides more reliable Redis connection.

> After publishing 1.5.0 release we've discovered that default HAProxy settings might cause intermittent failures.
> See [argo-cd#3358](https://github.com/argoproj/argo-cd/issues/3358)

#### Windows CLI

Windows users deploy to Kubernetes too! Now you can use Argo CD CLI on Linux, Mac OS, and Windows. The Windows compatible binary is available 
in the release details page as well as on the Argo CD Help page.

#### Breaking Changes

The `argocd_app_sync_status`, `argocd_app_health_status` and `argocd_app_created_time` prometheus metrics are deprecated in favor of additional labels
to `argocd_app_info` metric. The deprecated labels are still available can be re-enabled using `ARGOCD_LEGACY_CONTROLLER_METRICS=true` environment variable.
The legacy example Grafana dashboard is available at [examples/dashboard-legacy.json](https://github.com/argoproj/argo-cd/blob/master/examples/dashboard-legacy.json). 

####  Known issues
Last-minute bugs that will be addressed in 1.5.1 shortly:
 
* https://github.com/argoproj/argo-cd/issues/3336
* https://github.com/argoproj/argo-cd/issues/3319
* https://github.com/argoproj/argo-cd/issues/3339
* https://github.com/argoproj/argo-cd/issues/3358

#### Enhancements
* feat: support helm3 (#2383) (#3178)
* feat: Argo CD Service Account / Local Users #3185
* feat: Disable Admin Login (fixes #3019) (#3179)
* feat(ui): add docs to sync policy options present in create application panel (Close #3098) (#3203)
* feat: add "service-account" flag to "cluster add" command (#3183) (#3184)
* feat: Supports the validate-false option at an app level. Closes #1063 (#2542)
* feat: add dest cluster and namespace in the Events (#3093)
* feat: Rollback disables auto sync issue #2441 (#2591)
* feat: allow ssh and http repository references in bitbucketserver webhook #2773 (#3036)
* feat: Add helm --set-file support (#2751)
* feat: Include resource group for Event's InvolvedObject.APIVersion
* feat: Add argocd cmd for Windows #2121 (#3015)

#### Bug Fixes

- fix: app reconciliation fails with panic: index out of (#3233)
- fix: upgrade argoproj/pkg version to fix leaked sensitive information in logs (#3230)
- fix: set MaxCallSendMsgSize to MaxGRPCMessageSize for the GRPC caller (#3117)
- fix: stop caching helm index (#3193)
- fix: dex proxy should forward request to dex preserving the basehref (#3165)
- fix: set default login redirect to baseHRef (#3164)
- fix: don't double-prepend basehref to redirect URLs (fixes #3137)
- fix: ui referring to /api/version using absolute path (#3092)
- fix: Unhang UI on long app info items by using more sane URL match pattern (#3159)
- fix: Allow multiple hostnames per SSH known hosts entry and also allow IPv6 (#2814) (#3074)
- fix: argocd-util backup produced truncated backups. import app status (#3096)
- fix: upgrade redis-ha chart and enable haproxy (#3147)
- fix: make dex server deployment init container resilient to restarts (#3136)
- fix: redact secret values of manifests stored in git (#3088)
- fix: labels not being deleted via UI (#3081)
- fix: HTTP|HTTPS|NO_PROXY env variable reading #3055 (#3063)
- fix: Correct usage text for repo add command regarding insecure repos (#3068)
- fix: Ensure SSH private key is written out with a final newline character (#2890) (#3064)
- fix: Handle SSH URLs in 'git@server:org/repo' notation correctly (#3062)
- fix sso condition when several sso connectors has been configured (#3057)
- fix: Fix bug where the same pointer is used. (#3059)
- fix: Opening in new tab bad key binding on Linux (#3020)
- fix: K8s secrets for repository credential templates are not deleted when credential template is deleted (#3028)
- fix: SSH credential template not working #3016
- fix: Unable to parse kubectl pre-release version strings (#3034)
- fix: Jsonnet TLA parameters of same type are overwritten (#3022)
- fix: Replace aws-iam-authenticator to support IRSA (#3010)
- fix: Hide bindPW in dex config (#3025)
- fix: SSH repo URL with a user different from `git` is not matched correctly when resolving a webhook (#2988)
- fix: JWT invalid => Password for superuser has changed since token issued (#2108)

#### Contributors
* alexandrfox
* alexec
* alexmt
* bergur88
* CBytelabs
* dbeal-wiser 
* dnascimento
* Elgarni
* eSamS
* gpaul
* jannfis
* jdmulloy
* machgo
* masa213f
* matthyx
* rayanebel
* shelby-moore
* tomcruise81
* wecger
* zeph

## v1.4.2 (2020-01-24)

- fix: correctly replace cache in namespace isolation mode (#3023)

## v1.4.1 (2020-01-23)

- fix: impossible to config RBAC if group name includes ',' (#3013)

## v1.4.0 (2020-01-17)

The v1.4.0 is a stability release that brings multiple bug fixes, security, performance enhancements, and multiple usability improvements.

#### New Features

#### Security
A number of security enhancements and features have been implemented (thanks to [@jannfis](https://github.com/jannfis) for driving it! ):
* **Repository Credential Templates Management UI/CLI**. Now you can use Argo CD CLI or UI to configure
[credentials template](https://argoproj.github.io/argo-cd/user-guide/private-repositories/#credential-templates) for multiple repositories!
* **X-Frame-Options header on serving static assets**. The X-Frame-Options prevents third party sites to trick users into interacting with the application.
* **Tighten AppProject RBAC enforcement**. We've improved the enforcement of access rules specified in the
[application project](https://argoproj.github.io/argo-cd/operator-manual/declarative-setup/#projects) configuration.

#### Namespace Isolation
With the namespace isolation feature, you are no longer have to give full read-only cluster access to the Argo CD. Instead, you can give access only to selected namespaces with-in
the cluster:

```bash
argocd cluster add <mycluster> --namespace <mynamespace1> --namespace <mynamespace2>
```

This feature is useful if you don't have full cluster access but still want to use Argo CD to manage some cluster namespaces. The feature also improves performance if Argo CD is
used to manage a few namespaces of a large cluster.

#### Reconciliation Performance
The Argo CD no longer fork/exec `kubectl` to apply resource changes in the target cluster or convert resource manifest to the required manifest version. This reduces
CPU and Memory usage of large Argo CD instances.

#### Resources Health based Hook Status
The existing Argo CD [resource hooks](https://argoproj.github.io/argo-cd/user-guide/resource_hooks/) feature allows running custom logic during the syncing process. You can mark
any Kubernetes resource as a hook and Argo CD assess hook status if resource is a `Pod`, `Job` or `Argo Workflow`. In the v1.4.0 release Argo CD is going to leverage resource
[health assessment](https://argoproj.github.io/argo-cd/operator-manual/health/) to get sync hook status. This allows using any custom CRD as a sync hook and leverage custom health
check logic.

#### Manifest Generation
* **Track Helm Charts By Semantic Version**. You've been able to track charts hosted in Git repositories using branches to tags. This is now possible for Helm charts. You no longer
 need to choose the exact version, such as v1.4.0 ,instead you can use a semantic version constraint such as v1.4.* and the latest version that matches will be installed.
* **Build Environment Variables**. Feature allows config management tool to get access to app details during manifest generation via
[environment variables](https://argoproj.github.io/argo-cd/user-guide/build-environment/).
* **Git submodules**. Argo CD is going to automatically fetch sub-modules if your repository has `.gitmodules` directory.

#### UI and CLI
* **Improved Resource Tree View**. The Application details page got even prettier. The resource view was tuned to fit more resources into the screen, include more information about
each resource and don't lose usability at the same time.
* **New Account Management CLI Command**. The CLI allows to check which actions are allowed for your account: `argocd account can-i sync applications '*'`

#### Maintenance Tools
The team put more effort into building tools that help to maintain Argo CD itself:
* **Bulk Project Editing**. The `argocd-util` allows to add and remove permissions defined in multiple project roles using one command.
* **More Prometheus Metrics**. A set of additional metrics that contains useful information managed clusters is exposed by application controller.

More documentation and tools are coming in patch releases.

#### Breaking Changes

The Argo CD deletes all **in-flight** hooks if you terminate running sync operation. The hook state assessment change implemented in this release the Argo CD enables detection of 
an in-flight state for all Kubernetes resources including `Deployment`, `PVC`, `StatefulSet`, `ReplicaSet` etc. So if you terminate the sync operation that has, for example,
`StatefulSet` hook that is `Progressing` it will be deleted. The long-running jobs are not supposed to be used as a sync hook and you should consider using
[Sync Waves](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/) instead.

#### Enhancements
* feat: Add custom health checks for cert-manager v0.11.0 (#2689) 
* feat: add git submodule support (#2495)
* feat: Add repository credential management API and CLI (addresses #2136) (#2207)
* feat: add support for --additional-headers cli flag (#2467)
* feat: Add support for ssh-with-port repo url (#2866) (#2948)
* feat: Add Time to ApplicationCondition. (#2417)
* feat: Adds `argocd auth can-i` command. Close #2255
* feat: Adds revision history limit. Closes #2790 (#2818)
* feat: Adds support for ARGO_CD_[TARGET_REVISION|REVISION] and pass to Custom Tool/Helm/Jsonnet 
* feat: Adds support for Helm charts to be a semver range. Closes #2552 (#2606)
* feat: Adds tracing to key external invocations. (#2811)
* feat: argocd-util should allow editing project policies in bulk  (#2615)
* feat: Displays controllerrevsion's revision in the UI. Closes #2306 (#2702)
* feat: Issue #2559 - Add gauge Prometheus metric which represents the number of pending manifest requests. (#2658)
* feat: Make ConvertToVersion maybe 1090% faster on average (#2820)
* feat: namespace isolation (#2839)
* feat: removes redundant mutex usage in controller cache and adds cluster cache metrics (#2898)
* feat: Set X-Frame-Options on serving static assets (#2706) (#2711)
* feat: Simplify using Argo CD without users/SSO/UI (#2688)
* feat: Template Out Data Source in Grafana Dashboard (#2859) 
* feat: Updates UI icons. Closes #2625 and #2757 (#2653)
* feat: use editor arguments in InteractiveEditor (#2833)
* feat: Use kubectl apply library instead of forking binary (#2861)
* feat: use resource health for hook status evaluation (#2938)

#### Bug Fixes

- fix: Adds support for /api/v1/account* via HTTP. Fixes #2664 (#2701)
- fix: Allow '@'-character in SSH usernames when connecting a repository (#2612)
- fix: Allow dot in project policy. Closes #2724 (#2755)
- fix: Allow you to sync local Helm apps.  Fixes #2741 (#2747)
- fix: Allows Helm parameters that contains arrays or maps. (#2525)
- fix: application-controller doesn't deal with rm/add same cluster gracefully (x509 unknown) (#2389)
- fix: diff local ignore kustomize build options (#2942)
- fix: Ensures that Helm charts are correctly resolved before sync. Fixes #2758 (#2760)
- fix: Fix 'Open application' link when using basehref (#2729)
- fix: fix a bug with cluster add when token secret is not first in list. (#2744)
- fix: fix bug where manifests are not cached. Fixes #2770 (#2771)
- fix: Fixes bug whereby retry does not work for CLI. Fixes #2767 (#2768)
- fix: git contention leads applications into Unknown state (#2877)
- fix: Issue #1944 - Gracefully handle missing cached app state (#2464)
- fix: Issue #2668 - Delete a specified context (#2669)
- fix: Issue #2683 - Make sure app update don't fail due to concurrent modification (#2852)
- fix: Issue #2721 Optimize helm repo querying (#2816)
- fix: Issue #2853 - Improve application env variables/labels editing (#2856)
- fix: Issue 2848 - Application Deployment history panel shows incorrect info for recent releases (#2849)
- fix: Make BeforeHookCreation the default. Fixes #2754 (#2759)
- fix: No error on `argocd app create` in CLI if `--revision` is omitted #2665
- fix: Only delete resources during app delete cascade if permitted to (fixes #2693) (#2695)
- fix: prevent user from seeing/deleting resources not permitted in project (#2908) (#2910)
- fix: self-heal should retry syncing an application after specified delay
- fix: stop logging dex config secrets #(2904) (#2937)
- fix: stop using jsondiffpatch on clientside to render resource difference  (#2869)
- fix: Target Revision truncated #2736
- fix: UI should re-trigger SSO login if SSO JWT token expires (#2891)
- fix: update argocd-util import was not working properly (#2939)

#### Contributors

* Aalok Ahluwalia
* Aananth K
* Abhishek Jaisingh
* Adam Johnson
* Alan Tang
* Alex Collins
* Alexander Matyushentsev
* Andrew Waters
* Byungjin Park
* Christine Banek
* Daniel Helfand
* David Hong
* David J. M. Karlsen
* David Maciel
* Devan Goodwin
* Devin Stein
* dthomson25
* Gene Liverman
* Gregor Krmelj
* Guido Maria Serra
* Ilir Bekteshi
* Imran Ismail
* INOUE BANJI
* Isaac Gaskin
* jannfis
* Jeff Hastings
* Jesse Suen
* John Girvan
* Konstantin
* Lev Aminov
* Manatsawin Hanmongkolchai
* Marco Schmid
* Masayuki Ishii
* Michael Bridgen
* Naoki Oketani
* niqdev
* nitinpatil1992
* Olivier Boukili
* Olivier Lemasle
* Omer Kahani
* Paul Brit
* Qingbo Zhou
* Saradhi Sreegiriraju
* Scott Cabrinha
* shlo
* Simon Behar
* stgarf
* Yujun Zhang
* Zoltán Reegn

## v1.3.4 (2019-12-05)
- #2819 Fixes logging of tracing option in CLI

## v1.3.3 (2019-12-05)
- #2721 High CPU utilisation (5 cores) and spammy logs

## v1.3.2 (2019-12-03)
- #2797 Fix directory traversal edge case and enhance tests

## v1.3.1 (2019-12-02)
- #2664 update account password from API resulted 404
- #2724 Can't use `DNS-1123` compliant app name when creating project role
- #2726 App list does not show chart for Helm app
- #2741 argocd local sync cannot parse kubernetes version
- #2754 BeforeHookCreation should be the default hook
- #2767 Fix bug whereby retry does not work for CLI
- #2770 Always cache miss for manifests
- #1345 argocd-application-controller: can not retrieve list of objects using index : Index with name namespace does not exist

## v1.3.0 (2019-11-13)

#### New Features

##### Helm 1st-Class Support

We know that for many of our users, they want to deploy existing Helm charts using Argo CD. Up until now that has required you to create an Argo CD app in a Git repo that does nothing but point to that chart. Now you can use a Helm chart repository is the same way as a Git repository.

On top of that, we've improved support for Helm apps. The most common types of Helm hooks such as `pre-install` and `post-install` are supported as well as a the delete policy `before-hook-creation` which makes it easier to work with hooks.

https://youtu.be/GP7xtrnNznw

##### Orphan Resources

Some users would like to make sure that resources in a namespace are managed only by Argo CD. So we've introduced the concept of an "orphan resource" - any resource that is in namespace associated with an app, but not managed by Argo CD. This is enabled in the project settings. Once enabled, Argo CD will show in the app view any resources in the app's namespace that is not managed by Argo CD. 

https://youtu.be/9ZoTevVQf5I

##### Sync Windows

There may be instances when you want to control the times during which an Argo CD app can sync. Sync Windows now gives you the capability to create windows of time in which apps are either allowed or denied the ability to sync. This can apply to both manual and auto-sync, or just auto-sync. The windows are configured at the project level and assigned to apps using app name, namespace or cluster. Wildcards are supported for all fields.

#### Enhancements

* [UI] Add application labels to Applications list and Applications details page (#1099)
* Helm repository as first class Argo CD Application source (#1145)
* Ability to generate a warn/alert when a namespace deviates from the expected state (#1167)
* Improve diff support for resource requests/limits (#1615)
* HTTP API should allow JWT to be passed via Authorization header (#1642)
* Ability to create & upsert projects from spec (#1852)
* Support for in-line block from helm chart values (#1930)
* Request OIDC groups claim if groups scope is not supported (#1956)
* Add a maintenance window for Applications with automated syncing (#1995)
* Support `argocd.argoproj.io/hook-delete-policy: BeforeHookCreation` (#2036)
* Support setting Helm string parameters using CLI/UI (#2078)
* Config management plugin environment variable UI/CLI support (#2203)
* Helm: auto-detect URLs (#2260)
* Helm: UI improvements (#2261)
* Support `helm template --kube-version ` (#2275)
* Use community icons for resources (#2277)
* Make `group` optional for `ignoreDifferences` config (#2298)
* Update Helm docs (#2315)
* Add cluster information into Splunk (#2354)
* argocd list command should have filter options like by project (#2396)
* Add target/current revision to status badge (#2445)
* Update tooling to use Kustomize v3 (#2487)
* Update root `Dockerfile` to use the `hack/install.sh` (#2488)
* Support and document using HPA for repo-server (#2559)
* Upgrade Helm  (#2587)
* UI fixes for "Sync Apps" panel. (#2604)
* Upgrade kustomize from v3.1.0 to v3.2.1 (#2609)
* Map helm lifecycle hooks to ArgoCD pre/post/sync hooks (#355)
* [UI] Enhance app creation page with Helm parameters overrides (#1059)

#### Bug Fixes

- failed parsing on parameters with comma (#1660)
- StatefulSet with OnDelete Update Strategy stuck progressing (#1881)
- Warning during secret diffing (#1923)
- Error message "Unable to load data: key is missing" is confusing (#1944)
- OIDC group bindings are truncated (#2006)
- Multiple parallel app syncs causes OOM (#2022)
- Unknown error when setting params with argocd app set on helm app (#2046)
- Endpoint is no longer shown as a child of services (#2060)
- SSH known hosts entry cannot be deleted if contains shell pattern in name (#2099)
- Application 404s on names with periods (#2114)
- Adding certs for hostnames ending with a dot (.) is not possible (#2116)
- Fix `TestHookDeleteBeforeCreation` (#2141)
- v1.2.0-rc1 nil pointer dereference when syncing (#2146)
- Replacing services failure (#2150)
- 1.2.0-rc1 - Authentication Required error in Repo Server (#2152)
- v1.2.0-rc1 Applications List View doesn't work (#2174)
- Manual sync does not trigger Presync hooks (#2185)
- SyncError app condition disappears during app reconciliation (#2192)
- argocd app wait\sync prints 'Unknown' for resources without health (#2198)
- 1.2.0-rc2 Warning during secret diffing (#2206)
- SSO redirect url is incorrect if configured Argo CD URL has trailing slash (#2212)
- Application summary diff page shows hooks (#2215)
- An app with a single resource and Sync hook remains progressing (#2216)
- CONTRIBUTING documentation outdated (#2231)
- v1.2.0-rc2 does not retrieve http(s) based git repository behind the proxy (#2243)
- Intermittent "git ls-remote" request failures should not fail app reconciliation (#2245)
- Result of ListApps operation for Git repo is cached incorrectly (#2263)
- ListApps does not utilize cache (#2287)
- Controller panics due to nil pointer error (#2290)
- The Helm --kube-version support does not work on GKE: (#2303)
- Fixes bug that prevents you creating repos via UI/CLI.  (#2308)
- The 'helm.repositories' settings is dropped without migration path (#2316)
- Badge response does not contain cache control header (#2317)
- Inconsistent sync result from UI and CLI (#2321)
- Failed edit application with plugin type requiring environment (#2330)
- AutoSync doesn't work anymore (#2339)
- End-to-End tests not working with Kubernetes v1.16 (#2371)
- Creating an application from Helm repository should select "Helm" as source type (#2378)
- The parameters of ValidateAccess GRPC method should not be logged  (#2386)
- Maintenance window meaning is confusing (#2398)
- UI bug when targetRevision is omitted (#2407)
- Too many vulnerabilities in Docker image (#2425)
- proj windows commands not consistent with other commands (#2443)
- Custom resource actions cannot be executed from the UI (#2448)
- Application controller sometimes accidentally removes duplicated/excluded resource warning condition (#2453)
- Logic that checks sync windows state in the cli is incorrect (#2455)
- UI don't allow to create window with `* * * * *` schedule (#2475)
- Helm Hook is executed twice if annotated with both pre-install and pre-upgrade annotations (#2480)
- Impossible to edit chart name using App details page (#2484)
- ArgoCD does not provide CSRF protection (#2496)
- ArgoCD failing to install CRDs in master from Helm Charts (#2497)
- Timestamp in Helm package file name causes error in Application with Helm source (#2549)
- Attempting to create a repo with password but not username panics (#2567)
- UI incorrectly mark resources as `Required Pruning` (#2577)
- argocd app diff prints only first difference (#2616)
- Bump min client cache version (#2619)
- Cluster list page fails if any cluster is not reachable (#2620)
- Repository type should be mandatory for repo add command in CLI (#2622)
- Repo server executes unnecessary ls-remotes (#2626)
- Application list page incorrectly filter apps by label selector (#2633)
- Custom actions are disabled in Argo CD UI (#2635)
- Failure of `argocd version` in the self-building container image (#2645)
- Application list page is not updated automatically anymore (#2655)
- Login regression issues (#2659)
- Regression: Cannot return Kustomize version for 3.1.0 (#2662)
- API server does not allow creating role with action `action/*` (#2670)
- Application controller `kubectl-parallelism-limit` flag is broken (#2673)
- Annoying toolbar flickering (#2691)

## v1.2.5 (2019-10-29)

- Issue #2339 - Don't update `status.reconciledAt` unless compared with latest git version (#2581)

## v1.2.4 (2019-10-23)

- Issue #2185 - Manual sync don't trigger hooks (#2477)
- Issue #2339 - Controller should compare with latest git revision if app has changed (#2543)
- Unknown child app should not affect app health (#2544)
- Redact secrets in dex logs (#2538)

## v1.2.3 (2019-10-1)
* Make argo-cd docker images openshift friendly (#2362) (@duboisf)
* Add dest-server and dest-namespace field to reconciliation logs (#2354)
- Stop logging /repository.RepositoryService/ValidateAccess parameters (#2386)

## v1.2.2 (2019-09-26)
+ Resource action equivalent to `kubectl rollout restart` (#2177)
- Badge response does not contain cache-control header (#2317) (@greenstatic)
- Make sure the controller uses the latest git version if app reconciliation result expired (#2339)

## v1.2.1 (2019-09-12)
+ Support limiting number of concurrent kubectl fork/execs (#2022)
+ Add --self-heal flag to argocd cli (#2296)
- Fix degraded proxy support for http(s) git repository (#2243)
- Fix nil pointer dereference in application controller (#2290)

## v1.2.0 (2019-09-05)

### New Features

#### Server Certificate And Known Hosts Management

The Server Certificate And Known Hosts Management feature makes it really easy to connect private Git repositories to Argo CD. Now Argo CD provides UI and CLI which
enables managing certificates and known hosts which are used to access Git repositories. It is also possible to configure both hosts and certificates in a declarative manner using
[argocd-ssh-known-hosts-cm](https://github.com/argoproj/argo-cd/blob/master/docs/operator-manual/argocd-ssh-known-hosts-cm.yaml) and 
[argocd-tls-certs-cm.yaml](https://github.com/argoproj/argo-cd/blob/master/docs/operator-manual/argocd-tls-certs-cm.yaml) config maps.

#### Self-Healing

The existing Automatic Sync feature allows to automatically apply any new changes in Git to the target Kubernetes cluster. However, Automatic Sync does not cover the case when the
application is out of sync due to the unexpected change in the target cluster. The Self-Healing feature fills this gap. With Self-Healing enabled Argo CD automatically pushes the desired state from Git into the cluster every time when state deviation is detected.

**Anonymous access** - enable read-only access without authentication to anyone in your organization.

Support for Git LFS enabled repositories - now you can store Helm charts as tar files and enable Git LFS in your repository.

**Compact diff view** - compact diff summary of the whole application in a single view.

**Badge for application status** - add badge with the health and sync status of your application into README.md of your deployment repo.

**Allow configuring google analytics tracking** - use Google Analytics to check how many users are visiting UI or your Argo CD instance.

#### Backward Incompatible Changes
- Kustomize v1 support is removed. All kustomize charts are built using the same Kustomize version
- Kustomize v2.0.3 upgraded to v3.1.0 . We've noticed one backward incompatible change: https://github.com/kubernetes-sigs/kustomize/issues/42 . Starting v2.1.0 namespace prefix feature works with CRD ( which might cause renaming of generated resource definitions)
- Argo CD config maps must be annotated with `app.kubernetes.io/part-of: argocd` label. Make sure to apply updated `install.yaml` manifest in addition to changing image version.


#### Enhancements
+ Adds a floating action button with help and chat links to every page.… (#2124)
+ Enhances cookie warning with actual length to help users fix their co… (#2134)
+ Added 'SyncFail' to possible HookTypes in UI (#2147)
+ Support for Git LFS enabled repositories (#1853)
+ Server certificate and known hosts management (#1514)
+ Client HTTPS certificates for private git repositories (#1945)
+ Badge for application status (#1435)
+ Make the health check for APIService a built in (#1841)
+ Bitbucket Server and Gogs webhook providers (#1269)
+ Jsonnet TLA arguments in ArgoCD CLI (#1626)
+ Self Healing (#1736)
+ Compact diff view (#1831)
+ Allow Helm parameters to force ambiguously-typed values to be strings (#1846)
+ Support anonymous argocd access (#1620)
+ Allow configuring google analytics tracking (#738)
+ Bash autocompletion for argocd (#1798)
+ Additional commit metadata (#1219)
+ Displays targetRevision in app dashboards. (#1239)
+ Local path syncing (#839)
+ System level `kustomize build` options (#1789)
+ Adds support for `argocd app set` for Kustomize. (#1843)
+ Allow users to create tokens for projects where they have any role. (#1977)
+ Add Refresh button to applications table and card view (#1606)
+ Adds CLI support for adding and removing groups from project roles. (#1851)
+ Support dry run and hook vs. apply strategy during sync (#798)
+ UI should remember most recent selected tab on resource info panel (#2007)
+ Adds link to the project from the app summary page. (#1911)
+ Different icon for resources which require pruning (#1159)

#### Bug Fixes

- Do not panic if the type is not api.Status (an error scenario) (#2105)
- Make sure endpoint is shown as a child of service (#2060)
- Word-wraps app info in the table and list views. (#2004)
- Project source/destination removal should consider wildcards (#1780)
- Repo whitelisting in UI does not support wildcards (#2000)
- Wait for CRD creation during sync process (#1940)
- Added a button to select out of sync items in the sync panel (#1902)
- Proper handling of an excluded resource in an application (#1621)
- Stop repeating logs on stopped container (#1614)
- Fix git repo url parsing on application list view (#2174)
- Fix nil pointer dereference error during app reconciliation (#2146)
- Fix history api fallback implementation to support app names with dots (#2114)
- Fixes some code issues related to Kustomize build options. (#2146)
- Adds checks around valid paths for apps (#2133)
- Endpoint incorrectly considered top level managed resource (#2060)
- Allow adding certs for hostnames ending on a dot (#2116)

#### Other
* Upgrade kustomize to v3.1.0 (#2068)
* Remove support for Kustomize 1. (#1573)

#### Contributors

* [alexec](https://github.com/alexec)
* [alexmt](https://github.com/alexmt)
* [dmizelle](https://github.com/dmizelle)
* [lcostea](https://github.com/lcostea)
* [jutley](https://github.com/jutley)
* [masa213f](https://github.com/masa213f)
* [Rayyis](https://github.com/Rayyis)
* [simster7](https://github.com/simster7)
* [dthomson25](https://github.com/dthomson25)
* [jannfis](https://github.com/jannfis)
* [naynasiddharth](https://github.com/naynasiddharth)
* [stgarf](https://github.com/stgarf)


## v1.1.2 (2019-07-30)
- 'argocd app wait' should print correct sync status (#2049)
- Check that TLS is enabled when registering DEX Handlers (#2047)
- Do not ignore Argo hooks when there is a Helm hook. (#1952)

## v1.1.1 (2019-07-25)
+ Support 'override' action in UI/API (#1984)
- Fix argocd app wait message (#1982)

## v1.1.0 (2019-07-24)

### New Features

#### Sync Waves

Sync waves feature allows executing a sync operation in a number of steps or waves. Within each synchronization phase (pre-sync, sync, post-sync) you can have one or more waves,
than allows you to ensure certain resources are healthy before subsequent resources are synced.

#### Optimized Interaction With Git

Argo CD needs to execute `git fetch` operation to access application manifests and `git ls-remote` to resolve ambiguous git revision. The `git ls-remote` is executed very frequently
and although the operation is very lightweight it adds unnecessary load on Git server and might cause performance issues. In v1.1 release, the application reconciliation process was
optimized which significantly reduced the number of Git requests. With v1.1 release, Argo CD should send 3x ~ 5x fewer Git requests.

#### User Defined Application Metadata

User-defined Application metadata enables the user to define a list of useful URLs for their specific application and expose those links on the UI
(e.g. reference to a CI pipeline or an application-specific management tool). These links should provide helpful shortcuts that make easier to integrate Argo CD into existing
systems by making it easier to find other components inside and outside Argo CD.

### Deprecation Notice

* Kustomize v1.0 is deprecated and support will be removed in the Argo CD v1.2 release.

#### Enhancements

- Sync waves [#1544](https://github.com/argoproj/argo-cd/issues/1544)
- Adds Prune=false and IgnoreExtraneous options [#1629](https://github.com/argoproj/argo-cd/issues/1629)
- Forward Git credentials to config management plugins [#1628](https://github.com/argoproj/argo-cd/issues/1628)
- Improve Kustomize 2 parameters UI [#1609](https://github.com/argoproj/argo-cd/issues/1609)
- Adds `argocd logout` [#1210](https://github.com/argoproj/argo-cd/issues/1210)
- Make it possible to set Helm release name different from Argo CD app name.  [#1066](https://github.com/argoproj/argo-cd/issues/1066)
- Add ability to specify system namespace during cluster add operation [#1661](https://github.com/argoproj/argo-cd/pull/1661) 
- Make listener and metrics ports configurable [#1647](https://github.com/argoproj/argo-cd/pull/1647) 
- Using SSH keys to authenticate kustomize bases from git [#827](https://github.com/argoproj/argo-cd/issues/827)
- Adds `argocd app sync APPNAME --async` [#1728](https://github.com/argoproj/argo-cd/issues/1728)
- Allow users to define app specific urls to expose in the UI [#1677](https://github.com/argoproj/argo-cd/issues/1677)
- Error view instead of blank page in UI [#1375](https://github.com/argoproj/argo-cd/issues/1375)
- Project Editor: Whitelisted Cluster Resources doesn't strip whitespace [#1693](https://github.com/argoproj/argo-cd/issues/1693)
- Eliminate unnecessary git interactions for top-level resource changes (#1919)
- Ability to rotate the bearer token used to manage external clusters (#1084)

#### Bug Fixes

- Project Editor: Whitelisted Cluster Resources doesn't strip whitespace [#1693](https://github.com/argoproj/argo-cd/issues/1693)
- \[ui small bug\] menu position outside block [#1711](https://github.com/argoproj/argo-cd/issues/1711)
- UI will crash when create application without destination namespace [#1701](https://github.com/argoproj/argo-cd/issues/1701)
- ArgoCD synchronization failed due to internal error [#1697](https://github.com/argoproj/argo-cd/issues/1697)
- Replicasets ordering is not stable on app tree view [#1668](https://github.com/argoproj/argo-cd/issues/1668)
- Stuck processor on App Controller after deleting application with incomplete operation [#1665](https://github.com/argoproj/argo-cd/issues/1665)
- Role edit page fails with JS error [#1662](https://github.com/argoproj/argo-cd/issues/1662)
- failed parsing on parameters with comma [#1660](https://github.com/argoproj/argo-cd/issues/1660)
- Handle nil obj when processing custom actions [#1700](https://github.com/argoproj/argo-cd/pull/1700)
- Account for missing fields in Rollout HealthStatus [#1699](https://github.com/argoproj/argo-cd/pull/1699) 
- Sync operation unnecessary waits for a healthy state of all resources [#1715](https://github.com/argoproj/argo-cd/issues/1715)
- failed parsing on parameters with comma [#1660](https://github.com/argoproj/argo-cd/issues/1660)
- argocd app sync hangs when cluster is not configured (#1935)
- Do not allow app-of-app child app's Missing status to affect parent (#1954)
- Argo CD don't handle well k8s objects which size exceeds 1mb (#1685)
- Secret data not redacted in last-applied-configuration (#897)
- Running app actions requires only read privileges (#1827)
- UI should allow editing repo URL (#1763)
- Make status fields as optional fields (#1779)
- Use correct healthcheck for Rollout with empty steps list (#1776)

#### Other

- Add Prometheus metrics for git repo interactions (#1912)
- App controller should log additional information during app syncing (#1909)
- Make sure api server to repo server grpc calls have timeout (#1820)
- Forked tool processes should timeout (#1821)
- Add health check to the controller deployment (#1785)

#### Contributors

* [Aditya Gupta](https://github.com/AdityaGupta1)
* [Alex Collins](https://github.com/alexec)
* [Alex Matyushentsev](https://github.com/alexmt)
* [Danny Thomson](https://github.com/dthomson25)
* [jannfis](https://github.com/jannfis)
* [Jesse Suen](https://github.com/jessesuen)
* [Liviu Costea](https://github.com/lcostea)
* [narg95](https://github.com/narg95)
* [Simon Behar](https://github.com/simster7)

See also [milestone v1.1](https://github.com/argoproj/argo-cd/milestone/13)

## v1.0.0 (2019-05-16)

### New Features

#### Network View

A new way to visual application resources had been introduced to the Application Details page. The Network View visualizes connections between Ingresses, Services and Pods
based on ingress reference service, service's label selectors and labels. The new view is useful to understand the application traffic flow and troubleshot connectivity issues.

#### Custom Actions

Argo CD introduces Custom Resource Actions to allow users to provide their own Lua scripts to modify existing Kubernetes resources in their applications. These actions are exposed in the UI to allow easy, safe, and reliable changes to their resources.  This functionality can be used to introduce functionality such as suspending and enabling a Kubernetes cronjob, continue a BlueGreen deployment with Argo Rollouts, or scaling a deployment. 

#### UI Enhancements & Usability Enhancements

* New color palette intended to highlight unhealthily and out-of-sync resources more clearly.
* The health of more resources is displayed, so it easier to quickly zoom to unhealthy pods, replica-sets, etc.
* Resources that do not have health no longer appear to be healthy. 
* Support for configuring Git repo credentials at a domain/org level
* Support for configuring requested OIDC provider scopes and enforced RBAC scopes
* Support for configuring monitored resources whitelist in addition to excluded resources

### Breaking Changes

* Remove deprecated componentParameterOverrides field #1372

### Changes since v0.12.2

#### Enhancements

* `argocd app wait` should have `--resource` flag like sync #1206
* Adds support for `kustomize edit set image`. Closes #1275 (#1324)
* Allow wait to return on health or suspended (#1392)
* Application warning when a manifest is defined twice #1070
* Create new documentation website #1390
* Default view should resource view instead of diff view #1354
* Display number of errors on resource tab #1477
* Displays resources that are being deleted as "Progressing". Closes #1410 (#1426)
* Generate random name for grpc proxy unix socket file instead of time stamp (#1455)
* Issue #357 - Expose application nodes networking information (#1333)
* Issue #1404 - App controller unnecessary set namespace to cluster level resources (#1405)
* Nils health if the resource does not provide it. Closes #1383 (#1408)
* Perform health assessments on all resource nodes in the tree. Closes #1382 (#1422)
* Remove deprecated componentParameterOverrides field #1372
* Shows the health of the application. Closes #1433 (#1434)
* Surface Service/Ingress external IPs, hostname to application #908
* Surface pod status to tree view #1358
* Support for customizable resource actions as Lua scripts #86
* UI / API Errors Truncated, Time Out #1386
* UI Enhancement Proposals Quick Wins #1274
* Update argocd-util import/export to support proper backup and restore (#1328)
* Whitelisting repos/clusters in projects should consider repo/cluster permissions #1432
* Adds support for configuring repo creds at a domain/org level. (#1332)
* Implement whitelist option analogous to `resource.exclusions` (#1490)
* Added ability to sync specific labels from the command line (#1241)
* Improve rendering app image information (#1552)
* Add liveness probe to repo server/api servers (#1546)
* Support configuring requested OIDC provider scopes and enforced RBAC scopes (#1471)

#### Bug Fixes

- Don't compare secrets in the CLI, since argo-cd doesn't have access to their data (#1459)
- Dropdown menu should not have sync item for unmanaged resources #1357
- Fixes goroutine leak. Closes #1381 (#1457)
- Improve input style #1217
- Issue #908 - Surface Service/Ingress external IPs, hostname to application (#1347)
- kustomization fields are all mandatory #1504
- Resource node details is crashing if live resource is missing $1505
- Rollback UI is not showing correct ksonnet parameters in preview #1326
- See details of applications fails with "r.nodes is undefined" #1371
- UI fails to load custom actions is resource is not deployed #1502
- Unable to create app from private repo: x509: certificate signed by unknown authority (#1171)
- Fix hardcoded 'git' user in `util/git.NewClient` (#1555)
- Application controller becomes unresponsive (#1476)
- Load target resource using K8S if conversion fails (#1414)
- Can't ignore a non-existent pointer anymore (#1586)
- Impossible to sync to HEAD from UI if auto-sync is enabled (#1579)
- Application controller is unable to delete self-referenced app (#1570)
- Prevent reconciliation loop for self-managed apps (#1533)
- Controller incorrectly report health state of self managed application (#1557)
- Fix kustomize manifest generation crash is manifest has image without version (#1540)
- Supply resourceVersion to watch request to prevent reading of stale cache (#1605)

## v0.12.2 (2019-04-22)

### Changes since v0.12.1

- Fix racing condition in controller cache (#1498)
- "bind: address already in use" after switching to gRPC-Web (#1451)
- Annoying warning while using --grpc-web flag (#1420)
- Delete helm temp directories (#1446)
- Fix null pointer exception in secret normalization function (#1389)
- Argo CD should not delete CRDs(#1425)
- UI is unable to load cluster level resource manifest (#1429)

## v0.12.1 (2019-04-09)

### Changes since v0.12.0

- [UI] applications view blows up when user does not have  permissions (#1368)
- Add k8s objects circular dependency protection to getApp method (#1374)
- App controller unnecessary set namespace to cluster level resources (#1404)
- Changing SSO login URL to be a relative link so it's affected by basehref (#101) (@arnarg)
- CLI diff should take into account resource customizations (#1294)
- Don't try deleting application resource if it already has `deletionTimestamp` (#1406)
- Fix invalid group filtering in 'patch-resource' command (#1319)
- Fix null pointer dereference error in 'argocd app wait' (#1366)
- kubectl v1.13 fails to convert extensions/NetworkPolicy (#1012)
- Patch APIs are not audited (#1397)

+ 'argocd app wait' should fail sooner if app transitioned to Degraded state (#733)
+ Add mapping to new canonical Ingress API group - kubernetes 1.14 support (#1348) (@twz123)
+ Adds support for `kustomize edit set image`. (#1275)
+ Allow using any name for secrets which store cluster credentials (#1218)
+ Update argocd-util import/export to support proper backup and restore (#1048)

## v0.12.0 (2019-03-20)

### New Features

#### Improved UI

Many improvements to the UI were made, including:

* Table view when viewing applications
* Filters on applications
* Table view when viewing application resources
* YAML editor in UI
* Switch to text-based diff instead of json diff
* Ability to edit application specs

#### Custom Health Assessments (CRD Health)

Argo CD has long been able to perform health assessments on resources, however this could only
assess the health for a few native kubernetes types (deployments, statefulsets, daemonsets, etc...).
Now, Argo CD can be extended to gain understanding of any CRD health, in the form of Lua scripts.
For example, using this feature, Argo CD now understands the CertManager Certificate CRD and will
report a Degraded status when there are issues with the cert.

#### Configuration Management Plugins

Argo CD introduces Config Management Plugins to support custom configuration management tools other
than the set that Argo CD provides out-of-the-box (Helm, Kustomize, Ksonnet, Jsonnet). Using config
management plugins, Argo CD can be configured to run specified commands to render manifests. This
makes it possible for Argo CD to support other config management tools (kubecfg, kapitan, shell
scripts, etc...).

#### High Availability

Argo CD is now fully HA. A set HA of manifests are provided for users who wish to run Argo CD in
a highly available manner. NOTE: The HA installation will require at least three different nodes due
to pod anti-affinity roles in the specs.

#### Improved Application Source

* Support for Kustomize 2
* YAML/JSON/Jsonnet Directories can now be recursed
* Support for Jsonnet external variables and top-level arguments

#### Additional Prometheus Metrics

Argo CD provides the following additional prometheus metrics:
* Sync counter to track sync activity and results over time
* Application reconciliation (refresh) performance to track Argo CD performance and controller activity
* Argo CD API Server metrics for monitoring HTTP/gRPC requests

#### Fuzzy Diff Logic

Argo CD can now be configured to ignore known differences for resource types by specifying a json
pointer to the field path to ignore. This helps prevent OutOfSync conditions when a user has no
control over the manifests. Ignored differences can be configured either at an application level, 
or a system level, based on a group/kind.

#### Resource Exclusions

Argo CD can now be configured to completely ignore entire classes of resources group/kinds.
Excluding high-volume resources improves performance and memory usage, and reduces load and
bandwidth to the Kubernetes API server. It also allows users to fine-tune the permissions that
Argo CD needs to a cluster by preventing Argo CD from attempting to watch resources of that
group/kind.

#### gRPC-Web Support

The argocd CLI can be now configured to communicate to the Argo CD API server using gRPC-Web
(HTTP1.1) using a new CLI flag `--grpc-web`. This resolves some compatibility issues users were
experiencing with ingresses and gRPC (HTTP2), and should enable argocd CLI to work with virtually
any load balancer, ingress controller, or API gateway.

#### CLI features

Argo CD introduces some additional CLI commands:

* `argocd app edit APPNAME` - to edit an application spec using preferred EDITOR
* `argocd proj edit PROJNAME` - to edit an project spec using preferred EDITOR
* `argocd app patch APPNAME` - to patch an application spec
* `argocd app patch-resource APPNAME` - to patch a specific resource which is part of an application


### Breaking Changes

#### Label selector changes, dex-server rename

The label selectors for deployments were been renamed to use kubernetes common labels
(`app.kubernetes.io/name=NAME` instead of `app=NAME`). Since K8s deployment label selectors are
immutable, during an upgrade from v0.11 to v0.12, the old deployments should be deleted using
`--cascade=false` which allows the new deployments to be created without introducing downtime.
Once the new deployments are ready, the older replicasets can be deleted. Use the following
instructions to upgrade from v0.11 to v0.12 without introducing downtime:

```
# delete the deployments with cascade=false. this orphan the replicasets, but leaves the pods running
kubectl delete deploy --cascade=false argocd-server argocd-repo-server argocd-application-controller

# apply the new manifests and wait for them to finish rolling out
kubectl apply <new install manifests>
kubectl rollout status deploy/argocd-application-controller
kubectl rollout status deploy/argocd-repo-server
kubectl rollout status deploy/argocd-application-controller

# delete old replicasets which are using the legacy label
kubectl delete rs -l app=argocd-server
kubectl delete rs -l app=argocd-repo-server
kubectl delete rs -l app=argocd-application-controller

# delete the legacy dex-server which was renamed
kubectl delete deploy dex-server
```

#### Deprecation of spec.source.componentParameterOverrides

For declarative application specs, the `spec.source.componentParameterOverrides` field is now
deprecated in favor of application source specific config. They are replaced with new fields
specific to their respective config management. For example, a Helm application spec using the
legacy field:

```yaml
spec:
  source:
    componentParameterOverrides:
    - name: image.tag
      value: v1.2
```

should move to:

```yaml
spec:
  source:
    helm:
      parameters:
      - name: image.tag
        value: v1.2
```

Argo CD will automatically duplicate the legacy field values to the new locations (and vice versa)
as part of automatic migration. The legacy `spec.source.componentParameterOverrides` field will be
kept around for the v0.12 release (for migration purposes) and will be removed in the next Argo CD
release.

#### Removal of spec.source.environment and spec.source.valuesFiles

The `spec.source.environment` and `spec.source.valuesFiles` fields, which were deprecated in v0.11,
are now completely removed from the Application spec.


#### API/CLI compatibility

Due to API spec changes related to the deprecation of componentParameterOverrides, Argo CD v0.12
has a minimum client version of v0.12.0. Older CLI clients will be rejected.


### Changes since v0.11:
+ Improved UI
+ Custom Health Assessments (CRD Health)
+ Configuration Management Plugins
+ High Availability
+ Fuzzy Diff Logic
+ Resource Exclusions
+ gRPC-Web Support
+ CLI features
+ Additional prometheus metrics
+ Sample Grafana dashboard (#1277) (@hartman17)
+ Support for Kustomize 2
+ YAML/JSON/Jsonnet Directories can now be recursed
+ Support for Jsonnet external variables and top-level arguments
+ Optimized reconciliation performance for applications with very active resources (#1267)
+ Support a separate OAuth2 CLI clientID different from server (#1307)
+ argocd diff: only print to stdout, if there is a diff + exit code (#1288) (@marcb1)
+ Detection and handling of duplicated resource definitions (#1284)
+ Support kustomize apps with remote bases in private repos in the same host (#1264)
+ Support patching resource using REST API (#1186)
* Deprecate componentParameterOverrides in favor of source specific config (#1207)
* Support talking to Dex using local cluster address instead of public address (#1211)
* Use Recreate deployment strategy for controller (#1315)
* Honor OS environment variables for helm commands (#1306) (@1337andre)
* Disable CGO_ENABLED for server/controller binaries (#1286)
* Documentation fixes and improvements (@twz123, @yann-soubeyrand, @OmerKahani, @dulltz)
- Fix CRD creation/deletion handling (#1249)
- Git cloning via SSH was not verifying host public key (#1276)
- Fixed multiple goroutine leaks in controller and api-server
- Fix issue where `argocd app set -p` required repo privileges. (#1280)
- Fix local diff of non-namespaced resources. Also handle duplicates in local diff (#1289)
- Deprecated resource kinds from 'extensions' groups are not reconciled correctly (#1232)
- Fix issue where CLI would panic after timeout when cli did not have get permissions (#1209)
- invalidate repo cache on delete (#1182) (@narg95)

## v0.11.2 (2019-02-19)
+ Adds client retry. Fixes #959 (#1119)
- Prevent deletion hotloop (#1115)
- Fix EncodeX509KeyPair function so it takes in account chained certificates (#1137) (@amarruedo)
- Exclude metrics.k8s.io from watch (#1128)
- Fix issue where dex restart could cause login failures (#1114)
- Relax ingress/service health check to accept non-empty ingress list (#1053)
- [UI] Correctly handle empty response from repository/<repo>/apps API

## v0.11.1 (2019-01-18)
+ Allow using redis as a cache in repo-server (#1020)
- Fix controller deadlock when checking for stale cache (#1044)
- Namespaces are not being sorted during apply (#1038)
- Controller cache was susceptible to clock skew in managed cluster
- Fix ability to unset ApplicationSource specific parameters
- Fix force resource delete API (#1033)
- Incorrect PermissionDenied error during app creation when using project roles + user-defined RBAC (#1019)
- Fix `kubctl convert` issue preventing deployment of extensions/NetworkPolicy (#1012)
- Do not allow metadata.creationTimestamp to affect sync status (#1021)
- Graceful handling of clusters where API resource discovery is partially successful (#1018)
- Handle k8s resources circular dependency (#1016)
- Fix `app diff --local` command (#1008)

## v0.11.0 (2019-01-10)
This is Argo CD's biggest release ever and introduces a completely redesigned controller architecture.

### New Features

#### Performance & Scalability
The application controller has a completely redesigned architecture which improved performance and
scalability during application reconciliation.

This was achieved by introducing an in-memory, live state cache of lightweight Kubernetes object 
metadata. During reconciliation, the controller no longer performs expensive, in-line queries of app
related resources in K8s API server, instead relying on the metadata available in the live state 
cache. This dramatically improves performance and responsiveness, and is less burdensome to the K8s
API server.

#### Object relationship visualization for CRDs
With the new controller design, Argo CD is now able to understand ownership relationship between
*all* Kubernetes objects, not just the built-in types. This enables Argo CD to visualize
parent/child relationships between all kubernetes objects, including CRDs.

#### Multi-namespaced applications
During sync, Argo CD will now honor any explicitly set namespace in a manifest. Manifests without a
namespace will continue deploy to the "preferred" namespace, as specified in app's
`spec.destination.namespace`. This enables support for a class of applications which install to
multiple namespaces. For example, Argo CD can now install the
[prometheus-operator](https://github.com/helm/charts/tree/master/stable/prometheus-operator)
helm chart, which deploys some resources into `kube-system`, and others into the
`prometheus-operator` namespace.

#### Large application support
Full resource objects are no longer stored in the Application CRD object status. Instead, only
lightweight metadata is stored in the status, such as a resource's sync and health status.
This change enabled Argo CD to support applications with a very large number of resources 
(e.g. istio), and reduces the bandwidth requirements when listing applications in the UI.

#### Resource lifecycle hook improvements
Resource lifecycle hooks (e.g. PreSync, PostSync) are now visible/manageable from the UI.
Additionally, bare Pods with a restart policy of Never can now be used as a resource hook, as an
alternative to Jobs, Workflows.

#### K8s recommended application labels
The tracking label for resources has been changed to use `app.kubernetes.io/instance`, as
recommended in [Kubernetes recommended labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/),
(changed from `applications.argoproj.io/app-name`). This will enable applications managed by Argo CD
to interoperate with other tooling which are also converging on this labeling, such as the
Kubernetes dashboard. Additionally, Argo CD no longer injects any tracking labels at the
`spec.template.metadata` level.

#### External OIDC provider support
Argo CD now supports auth delegation to an existing, external OIDC providers without the need for
running Dex (e.g. Okta, OneLogin, Auth0, Microsoft, etc...)

The optional, [Dex IDP OIDC provider](https://github.com/dexidp/dex) is still bundled as part of the
default installation, in order to provide a seamless out-of-box experience, enabling Argo CD to
integrate with non-OIDC providers, and to benefit from Dex's full range of
[connectors](https://dexidp.io/docs/connectors/).

#### OIDC group bindings to Project Roles
OIDC group claims from an OAuth2 provider can now be bound to a Argo CD project roles. Previously,
group claims could only be managed in the centralized ConfigMap, `argocd-rbac-cm`. They can now be
managed at a project level. This enables project admins to self service access to applications
within a project.

#### Declarative Argo CD configuration
Argo CD settings can be now be configured either declaratively, or imperatively. The `argocd-cm`
ConfigMap now has a `repositories` field, which can reference credentials in a normal Kubernetes
secret which you can create declaratively, outside of Argo CD.

#### Helm repository support
Helm repositories can be configured at the system level, enabling the deployment of helm charts
which have a dependency to external helm repositories.

### Breaking changes:

* Argo CD's resource names were renamed for consistency. For example, the application-controller
  deployment was renamed to argocd-application-controller. When upgrading from v0.10 to v0.11,
  the older resources should be pruned to avoid inconsistent state and controller in-fighting.

* As a consequence to moving to recommended kubernetes labels, when upgrading from v0.10 to v0.11,
  all applications will immediately be OutOfSync due to the change in tracking labels. This will
  correct itself with another sync of the application. However, since Pods will be recreated, please
  take this into consideration, especially if your applications are configured with auto-sync.

* There was significant reworking of the `app.status` fields to reduce the payload size, simplify
  the datastructure and remove fields which were no longer used by the controller. No breaking
  changes were made in `app.spec`.

* An older Argo CD CLI (v0.10 and below) will not be compatible with Argo CD v0.11. To keep
  CI pipelines in sync with the API server, it is recommended to have pipelines download the CLI
  directly from the API server https://${ARGOCD_SERVER}/download/argocd-linux-amd64 during the CI
  pipeline.

### Changes since v0.10:
* Improve Application state reconciliation performance (#806)
* Refactor, consolidate and rename resource type data structures
+ Declarative setup and configuration of ArgoCD (#536)
+ Declaratively add helm repositories (#747)
+ Switch to k8s recommended app.kubernetes.io/instance label (#857)
+ Ability for a single application to deploy into multiple namespaces (#696)
+ Self service group access to project applications (#742)
+ Support for Pods as a sync hook (#801)
+ Support 'crd-install' helm hook (#355)
+ Use external 'diff' utility to render actual vs target state difference
+ Show sync policy in app list view
* Remove resources state from application CRD (#758)
* API server & UI should serve argocd binaries instead of linking to GitHub (#716)
* Update versions for kubectl (v1.13.1), helm (v2.12.1), ksonnet (v0.13.1)
* Update version of aws-iam-authenticator (0.4.0-alpha.1)
* Ability to force refresh of application manifests from git
* Improve diff assessment for Secrets, ClusterRoles, Roles
- Failed to deploy helm chart with local dependencies and no internet access (#786)
- Out of sync reported if Secrets with stringData are used (#763)
- Unable to delete application in K8s v1.12 (#718)

## v0.10.6 (2018-11-14)
- Fix issue preventing in-cluster app sync due to go-client changes (issue #774)

## v0.10.5 (2018-11-13)
+ Increase concurrency of application controller
* Update dependencies to k8s v1.12 and client-go v9.0 (#729)
- add argo cluster permission to view logs (#766) (@conorfennell)
- Fix issue where applications could not be deleted on k8s v1.12
- Allow 'syncApplication' action to reference target revision rather then hard-coding to 'HEAD' (#69) (@chrisgarland)
- Issue #768 - Fix application wizard crash

## v0.10.4 (2018-11-07)
* Upgrade to Helm v0.11.0 (@amarrella)
- Health check is not discerning apiVersion when assessing CRDs (issue #753)
- Fix nil pointer dereference in util/health (@mduarte)

## v0.10.3 (2018-10-28)
* Fix applying TLS version settings
* Update to kustomize 1.0.10 (@twz123)

## v0.10.2 (2018-10-25)
* Update to kustomize 1.0.9 (@twz123)
- Fix app refresh err when k8s patch is too slow

## v0.10.1 (2018-10-24)

- Handle case where OIDC settings become invalid after dex server restart (issue #710)
- git clean also needs to clean files under gitignore (issue #711)

## v0.10.0 (2018-10-19)

### Changes since v0.9:

+ Allow more fine-grained sync (issue #508)
+ Display init container logs (issue #681)
+ Redirect to /auth/login instead of /login when SSO token is used for authentication (issue #348)
+ Support ability to use a helm values files from a URL (issue #624)
+ Support public not-connected repo in app creation UI (issue #426)
+ Use ksonnet CLI instead of ksonnet libs (issue #626)
+ We should be able to select the order of the `yaml` files while creating a Helm App (#664)
* Remove default params from app history (issue #556)
* Update to ksonnet v0.13.0
* Update to kustomize 1.0.8
- API Server fails to return apps due to grpc max message size limit  (issue #690)
- App Creation UI for Helm Apps shows only files prefixed with `values-` (issue #663)
- App creation UI should allow specifying values files outside of helm app directory bug (issue #658)
- argocd-server logs credentials in plain text when adding git repositories (issue #653)
- Azure Repos do not work as a repository (issue #643)
- Better update conflict error handing during app editing (issue #685)
- Cluster watch needs to be restarted when CRDs get created (issue #627)
- Credentials not being accepted for Google Source Repositories (issue #651)
- Default project is created without permission to deploy cluster level resources (issue #679)
- Generate role token click resets policy changes (issue #655)
- Input type text instead of password on Connect repo panel (issue #693)
- Metrics endpoint not reachable through the metrics kubernetes service (issue #672)
- Operation stuck in 'in progress' state if application has no resources (issue #682)
- Project should influence options for cluster and namespace during app creation (issue #592)
- Repo server unable to execute ls-remote for private repos (issue #639)
- Resource is always out of sync if it has only 'ksonnet.io/component' label (issue #686)
- Resource nodes are 'jumping' on app details page (issue #683)
- Sync always suggest using latest revision instead of target UI bug (issue #669)
- Temporary ignore service catalog resources (issue #650)

## v0.9.2 (2018-09-28)

* Update to kustomize 1.0.8
- Fix issue where argocd-server logged credentials in plain text during repo add (issue #653)
- Credentials not being accepted for Google Source Repositories (issue #651)
- Azure Repos do not work as a repository (issue #643)
- Temporary ignore service catalog resources (issue #650)
- Normalize policies by always adding space after comma

## v0.9.1 (2018-09-24)

- Repo server unable to execute ls-remote for private repos (issue #639)

## v0.9.0 (2018-09-24)

### Notes about upgrading from v0.8
* Cluster wide resources should be allowed in default project (due to issue #330):

```
argocd project allow-cluster-resource default '*' '*'
```

* Projects now provide the ability to allow or deny deployments of cluster-scoped resources
(e.g. Namespaces, ClusterRoles, CustomResourceDefinitions). When upgrading from v0.8 to v0.9, to
match the behavior of v0.8 (which did not have restrictions on deploying resources) and continue to
allow deployment of cluster-scoped resources, an additional command should be run:

```bash
argocd proj allow-cluster-resource default '*' '*'
```

The above command allows the `default` project to deploy any cluster-scoped resources which matches
the behavior of v0.8.

* The secret keys in the argocd-secret containing the TLS certificate and key, has been renamed from
  `server.crt` and `server.key` to the standard `tls.crt` and `tls.key` keys. This enables Argo CD
  to integrate better with Ingress and cert-manager. When upgrading to v0.9, the `server.crt` and
  `server.key` keys in argocd-secret should be renamed to the new keys.

### Changes since v0.8:
+ Auto-sync option in application CRD instance (issue #79)
+ Support raw jsonnet as an application source (issue #540)
+ Reorder K8s resources to correct creation order (issue #102)
+ Redact K8s secrets from API server payloads (issue #470)
+ Support --in-cluster authentication without providing a kubeconfig (issue #527)
+ Special handling of CustomResourceDefinitions (issue #613)
+ Argo CD should download helm chart dependencies (issue #582)
+ Export Argo CD stats as prometheus style metrics (issue #513)
+ Support restricting TLS version (issue #609)
+ Use 'kubectl auth reconcile' before 'kubectl apply' (issue #523)
+ Projects need controls on cluster-scoped resources (issue #330)
+ Support IAM Authentication for managing external K8s clusters (issue #482)
+ Compatibility with cert manager (issue #617)
* Enable TLS for repo server (issue #553)
* Split out dex into it's own deployment (instead of sidecar) (issue #555)
+ [UI] Support selection of helm values files in App creation wizard (issue #499)
+ [UI] Support specifying source revision in App creation wizard allow (issue #503)
+ [UI] Improve resource diff rendering (issue #457)
+ [UI] Indicate number of ready containers in pod (issue #539)
+ [UI] Indicate when app is overriding parameters (issue #503)
+ [UI] Provide a YAML view of resources (issue #396)
+ [UI] Project Role/Token management from UI (issue #548)
+ [UI] App creation wizard should allow specifying source revision (issue #562)
+ [UI] Ability to modify application from UI (issue #615)
+ [UI] indicate when operation is in progress or has failed (issue #566)
- Fix issue where changes were not pulled when tracking a branch (issue #567)
- Lazy enforcement of unknown cluster/namespace restricted resources (issue #599)
- Fix controller hot loop when app source contains bad manifests (issue #568)
- Fix issue where Argo CD fails to deploy when resources are in a K8s list format (issue #584)
- Fix comparison failure when app contains unregistered custom resource (issue #583)
- Fix issue where helm hooks were being deployed as part of sync (issue #605)
- Fix race conditions in kube.GetResourcesWithLabel and DeleteResourceWithLabel (issue #587)
- [UI] Fix issue where projects filter does not work when application got changed
- [UI] Creating apps from directories is not obvious (issue #565)
- Helm hooks are being deployed as resources (issue #605)
- Disagreement in three way diff calculation (issue #597)
- SIGSEGV in kube.GetResourcesWithLabel (issue #587)
- Argo CD fails to deploy resources list (issue #584)
- Branch tracking not working properly (issue #567)
- Controller hot loop when application source has bad manifests (issue #568)

## v0.8.2 (2018-09-12)
- Downgrade ksonnet from v0.12.0 to v0.11.0 due to quote unescape regression
- Fix CLI panic when performing an initial `argocd sync/wait`

## v0.8.1 (2018-09-10)
+ [UI] Support selection of helm values files in App creation wizard (issue #499)
+ [UI] Support specifying source revision in App creation wizard allow (issue #503)
+ [UI] Improve resource diff rendering (issue #457)
+ [UI] Indicate number of ready containers in pod (issue #539)
+ [UI] Indicate when app is overriding parameters (issue #503)
+ [UI] Provide a YAML view of resources (issue #396)
- Fix issue where changes were not pulled when tracking a branch (issue #567)
- Fix controller hot loop when app source contains bad manifests (issue #568)
- [UI] Fix issue where projects filter does not work when application got changed

## v0.8.0 (2018-09-04)

### Notes about upgrading from v0.7
* The RBAC model has been improved to support explicit denies. What this means is that any previous
RBAC policy rules, need to be rewritten to include one extra column with the effect:
`allow` or `deny`. For example, if a rule was written like this:
    ```
    p, my-org:my-team, applications, get, */*
    ```
    It should be rewritten to look like this:
    ```
    p, my-org:my-team, applications, get, */*, allow
    ```

### Changes since v0.7:
+ Support kustomize as an application source (issue #510)
+ Introduce project tokens for automation access (issue #498)
+ Add ability to delete a single application resource to support immutable updates (issue #262)
+ Update RBAC model to support explicit denies (issue #497)
+ Ability to view Kubernetes events related to application projects for auditing
+ Add PVC healthcheck to controller (issue #501)
+ Run all containers as an unprivileged user (issue #528)
* Upgrade ksonnet to v0.12.0
* Add readiness probes to API server (issue #522)
* Use gRPC error codes instead of fmt.Errorf (#532)
- API discovery becomes best effort when partial resource list is returned (issue #524)
- Fix `argocd app wait` printing incorrect Sync output (issue #542)
- Fix issue where argocd could not sync to a tag (#541)
- Fix issue where static assets were browser cached between upgrades (issue #489)

## v0.7.2 (2018-08-21)
- API discovery becomes best effort when partial resource list is returned (issue #524)

## v0.7.1 (2018-08-03)
+ Surface helm parameters to the application level (#485)
+ [UI] Improve application creation wizard (#459)
+ [UI] Show indicator when refresh is still in progress (#493)
* [UI] Improve data loading error notification (#446)
* Infer username from claims during an `argocd relogin` (#475)
* Expand RBAC role to be able to create application events. Fix username claims extraction
- Fix scalability issues with the ListApps API (#494)
- Fix issue where application server was retrieving events from incorrect cluster (#478)
- Fix failure in identifying app source type when path was '.'
- AppProjectSpec SourceRepos mislabeled (#490)
- Failed e2e test was not failing CI workflow
* Fix linux download link in getting_started.md (#487) (@chocopowwwa)

## v0.7.0 (2018-07-27)
+ Support helm charts and yaml directories as an application source
+ Audit trails in the form of API call logs
+ Generate kubernetes events for application state changes
+ Add ksonnet version to version endpoint (#433)
+ Show CLI progress for sync and rollback
+ Make use of dex refresh tokens and store them into local config
+ Expire local superuser tokens when their password changes
+ Add `argocd relogin` command as a convenience around login to current context
- Fix saving default connection status for repos and clusters
- Fix undesired fail-fast behavior of health check
- Fix memory leak in the cluster resource watch
- Health check for StatefulSets, DaemonSet, and ReplicaSets were failing due to use of wrong converters

## v0.6.2 (2018-07-23)
- Health check for StatefulSets, DaemonSet, and ReplicaSets were failing due to use of wrong converters

## v0.6.1 (2018-07-18)
- Fix regression where deployment health check incorrectly reported Healthy
+ Intercept dex SSO errors and present them in Argo login page

## v0.6.0 (2018-07-16)
+ Support PreSync, Sync, PostSync resource hooks
+ Introduce Application Projects for finer grain RBAC controls
+ Swagger Docs & UI
+ Support in-cluster deployments internal kubernetes service name
+ Refactoring & Improvements
* Improved error handling, status and condition reporting
* Remove installer in favor of kubectl apply instructions
* Add validation when setting application parameters
* Cascade deletion is decided during app deletion, instead of app creation
- Fix git authentication implementation when using using SSH key
- app-name label was inadvertently injected into spec.selector if selector was omitted from v1beta1 specs

## v0.5.4 (2018-06-27)
- Refresh flag to sync should be optional, not required

## v0.5.3 (2018-06-20)
+ Support cluster management using the internal k8s API address https://kubernetes.default.svc (#307)
+ Support diffing a local ksonnet app to the live application state (resolves #239) (#298)
+ Add ability to show last operation result in app get. Show path in app list -o wide (#297)
+ Update dependencies: ksonnet v0.11, golang v1.10, debian v9.4 (#296)
+ Add ability to force a refresh of an app during get (resolves #269) (#293)
+ Automatically restart API server upon certificate changes (#292)

## v0.5.2 (2018-06-14)
+ Resource events tab on application details page (#286)
+ Display pod status on application details page (#231)

## v0.5.1 (2018-06-13)
- API server incorrectly compose application fully qualified name for RBAC check (#283)
- UI crash while rendering application operation info if operation failed

## v0.5.0 (2018-06-12)
+ RBAC access control
+ Repository/Cluster state monitoring
+ Argo CD settings import/export
+ Application creation UI wizard
+ argocd app manifests for printing the application manifests
+ argocd app unset command to unset parameter overrides
+ Fail app sync if prune flag is required (#276)
+ Take into account number of unavailable replicas to decided if deployment is healthy or not #270
+ Add ability to show parameters and overrides in CLI (resolves #240)
- Repo names containing underscores were not being accepted (#258)
- Cookie token was not parsed properly when mixed with other site cookies

## v0.4.7 (2018-06-07)
- Fix argocd app wait health checking logic

## v0.4.6 (2018-06-06)
- Retry argocd app wait connection errors from EOF watch. Show detailed state changes

## v0.4.5 (2018-05-31)
+ Add argocd app unset command to unset parameter overrides
- Cookie token was not parsed properly when mixed with other site cookies

## v0.4.4 (2018-05-30)
+ Add ability to show parameters and overrides in CLI (resolves #240)
+ Add Events API endpoint
+ Issue #238 - add upsert flag to 'argocd app create' command
+ Add repo browsing endpoint (#229)
+ Support subscribing to settings updates and auto-restart of dex and API server
- Issue #233 - Controller does not persist rollback operation result
- App sync frequently fails due to concurrent app modification

## v0.4.3 (2018-05-21)
- Move local branch deletion as part of git Reset() (resolves #185) (#222)
- Fix exit code for app wait (#219)

## v0.4.2 (2018-05-21)
+ Show URL in argocd app get
- Remove interactive context name prompt during login which broke login automation
* Rename force flag to cascade in argocd app delete

## v0.4.1 (2018-05-18)
+ Implemented argocd app wait command

## v0.4.0 (2018-05-17)
+ SSO Integration
+ GitHub Webhook
+ Add application health status
+ Sync/Rollback/Delete is asynchronously handled by controller
* Refactor CRUD operation on clusters and repos
* Sync will always perform kubectl apply
* Synced Status considers last-applied-configuration annotation
* Server & namespace are mandatory fields (still inferred from app.yaml)
* Manifests are memoized in repo server
- Fix connection timeouts to SSH repos

## v0.3.2 (2018-05-03)
+ Application sync should delete 'unexpected' resources #139
+ Update ksonnet to v0.10.1
+ Detect unexpected resources
- Fix: App sync frequently fails due to concurrent app modification #147
- Fix: improve app state comparator: #136, #132

## v0.3.1 (2018-04-24)
+ Add new rollback RPC with numeric identifiers
+ New argo app history and argo app rollback command
+ Switch to gogo/protobuf for golang code generation
- Fix: create .argocd directory during argo login (issue #123)
- Fix: Allow overriding server or namespace separately (issue #110)

## v0.3.0 (2018-04-23)
+ Auth support
+ TLS support
+ DAG-based application view
+ Bulk watch
+ ksonnet v0.10.0-alpha.3
+ kubectl apply deployment strategy
+ CLI improvements for app management

## v0.2.0 (2018-04-03)
+ Rollback UI
+ Override parameters

## v0.1.0 (2018-03-12)
+ Define app in GitHub with dev and preprod environment using KSonnet
+ Add cluster Diff App with a cluster Deploy app in a cluster
+ Deploy a new version of the app in the cluster
+ App sync based on GitHub app config change - polling only
+ Basic UI: App diff between Git and k8s cluster for all environments Basic GUI
