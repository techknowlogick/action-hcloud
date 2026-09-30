# GitHub Actions for Hetzner Cloud

This action enables you to interact with [Hetzner Cloud](https://www.hetzner.com/cloud) services by installing [the `hcloud` command-line client](https://github.com/hetznercloud/cli/).

## Usage

To install the latest version of `hcloud` and use it in GitHub Actions workflows, add the following step:

```yaml
    - name: Install hcloud
      uses: techknowlogick/action-hcloud@v3
      with:
        token: ${{ secrets.HCLOUD_TOKEN }}

    - run: hcloud server list
```

To install a specific version instead:

```yaml
    - name: Install hcloud
      uses: techknowlogick/action-hcloud@v3
      with:
        token: ${{ secrets.HCLOUD_TOKEN }}
        version: 1.40.0
```

`hcloud` will now be available on the `PATH`, and the token is exported as `HCLOUD_TOKEN`, so later steps in the same job can use `hcloud` directly. The token is masked in logs. The action checks the token by running `hcloud datacenter list`, and fails if the token is invalid.

The token is optional. Without it, the action only installs the CLI, and you can pass credentials to later steps yourself.

The action supports Linux, macOS and Windows runners on x64 and arm64. Each download is checked against the release's published SHA-256 checksums.

### Inputs

- `token` – (Optional) A Hetzner Cloud API token. If set, it is checked and exported for later steps. Leave it out to only install the CLI.
- `version` – (Optional) The version of `hcloud` to install, e.g. `1.40.0`. Defaults to the latest release.
- `github-token` – (Optional) Token used to look up `hcloud` releases on GitHub. Defaults to the workflow's `GITHUB_TOKEN` on github.com, which avoids the unauthenticated API rate limit.

### Outputs

- `version` – The version of `hcloud` that was installed.

## Contributing

To install the needed dependencies, run `npm ci`. The resulting `node_modules/` directory _is not_ checked in to Git.

Run `npm test` to lint the code and run the unit tests.

Before submitting a pull request, run `npm run package` to package the code [using `ncc`](https://github.com/vercel/ncc). Packaging assembles the code including dependencies into the `dist/` directory, which is checked in to Git.

Pull requests should be made against the `v2` branch.

## License

This GitHub Action and associated scripts and documentation in this project are released under the [MIT License](LICENSE).

## Credits

Forked from DigitalOcean's [doctl action](https://github.com/digitalocean/action-doctl).
