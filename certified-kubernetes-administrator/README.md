# Certified Kubernetes Administrator (CKA)

everything you need to ace the CKA

video versions:
- [youtube](https://youtu.be/8VK9NJ3pObU)
- [odysee](https://odysee.com/cka:2d91419bbe07773faed5966e96cd8281b5c3d80c?r=9f3WxR2Dzb1gykXgcuMxPbtww1a2MXhP)

## intro
- took the June 2022 updated version of the CKA
- ~1 month of general study with 3 days of exam prep
- 120 minute exam, had ~50 minutes after my first passthrough
- passed with a score of 91% (66% pass threshold)

## outline
- how to study
- the testing environment
- finesse guide

## how to study

- complete a course
  - [acloudguru CKA](https://acloudguru.com/course/certified-kubernetes-administrator-cka) is good but the scenarios are too easy
  - the internet recommends [kodecloud's course by Mumshad Mannambeth](https://kodekloud.com/courses/certified-kubernetes-administrator-cka/)
- [killer.sh](https://killer.sh/)
  - 2 free runs with exam purchase
  - do ONCE (timed) then REVIEW
  - the explanations are very well done, read them all.
  - [UPDATE: july 2022](https://twitter.com/_killer_shell/status/1548205851940229120?s=20&t=O9b0xhvhWuaOwRVAkKsRzQ) now in a remote desktop like the updated exam!
- [killer coda scenarios](https://killercoda.com/killer-shell-cka)
  - do each one and read the explanations

## the testing environment
![interface](https://miro.medium.com/max/875/1*EzwMAPg4-XuBBWqt6WTmLQ.png)

[source: Kim Wuestkamp on itnext.io](https://itnext.io/cks-cka-ckad-changed-terminal-to-remote-desktop-157a26c1d5e)

- checkin process
  - ID check and camera scan
  - clean your testing area
  - one monitor
  - don't stress
- moved to remote desktop environment in June 2022
  - XFCE, Firefox
  - expect some lag
  - multiple terminals and browser tabs allowed
  - keyboard layout preserved
- copy/paste
  - right click menu
  - ctrl-shift-(c|v)
  - one-click copy from instructions (recommended to avoid typos)
  - copying from firefox will trigger a warning (and maybe miss a character)
- terminal
  - `kubectl` is pre-aliased to `k` with autocompletion
  - `.vimrc` is pre-set (no need to remember) `shiftwidth=2; expandtab=true; tabstop=2`
  - vscode and webstorm available as well [more here](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface#virtual-machine-jsnad-and-jsnsd-exams-only)
  - `tmux` available but not necessary
- misc recommendations
  - use a big screen
  - hide the PSI top bar
  - maximize your comfort

## finesse guide

### mindset
- time is your most valuable resource, speed is your best friend
- be imperative first, declarative second

### `k create|run ... -h`
- copying yaml from docs is LAST RESORT
  - just make the thing with `k create|run`
  - add `... --dry-run=client -o yaml > resource.yaml` if you need to add things before apply
- use the `-h` option
  - tells you EXACTLY what can be created imperatively WITH EXAMPLES
  - menu increases in detail with base command

### understand [the k8s docs](https://kubernetes.io/docs/home/)
- remember important pages and examples
  - mentally bookmark templates that can't be created interactively (pv, pvc, netpol, etc.)
- ctrl-f `kind: <MY RESOURCE>` to quickly find example yaml
- use the [one-pager api reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/) for specific details

### use shortnames
- never type out a full resource name if you can help it
  - cm -> configmap
  - pvc -> persistentvolumeclaim
  - ...
- check all shortnames with `k api-resources`

### aliases, functions, and variables
- memorize what you think you'll use

```{bash}
# IMHO must-haves

## create yaml on-the-fly faster
export do='--dry-run=client -o yaml'

## organize your files per question #
mkcd() { mkdir -p "$@" && cd "$@" ; }
```

```{bash}
# nice to haves

## create/destroy from yaml faster
alias kaf='k apply -f '
alias kdf='k destroy -f '

## namespaces (poor man's `kubens`)
export nk='-n kube-system'
export n='-n important-ns' # set this as needed

## destroy things without waiting
export now='--grace-period 0 --force'
```
