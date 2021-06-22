# Skopeo

Pull image from docker hub

```bash
$ skopeo copy docker://docker.io/nginx:latest containers-storage:test/nginx
$ podman images
docker.io/test/nginx          latest  d1a364dc548d  3 weeks ago   137 MB
```

Pull image from docker hub to local directories

```bash
$ skopeo copy docker://docker.io/nginx:latest dir:nginx-copy
$ tree nginx-copy
nginx-copy/
├── 30afc0b18f67ae8441c2d26e356693009bb8927ab7e3bce05d5ed99531c9c1d4
├── 351ad75a6cfabc7f2e103963945ff803d818f0bdcf604fd2072a0eefd6674bde
├── 596b1d696923618bec6ff5376cc9aed03a3724bc75b6c03221fd877b62046d05
├── 69692152171afee1fd341febc390747cfca2ff302f2881d8b394e786af605696
├── 8283eee92e2f756bd57f96ea295e332ab9031724267d4f939de1f7d19fe9611a
├── d1a364dc548d5357f0da3268c888e1971bbdb957ee3f028fe7194f1d61c6fdee
├── febe5bd23e98102ed5ff64b8f5987f516a945745c08bbcf2c61a50fb6e7b2257
├── manifest.json
└── version

0 directories, 9 files
```

Pull image from docker hub to local OCI-layout directories

```bash
$ skopeo copy docker://docker.io/nginx:latest oci:nginx-copy-oci
$ tree nginx-copy-oci
nginx-copy-oci/
├── blobs
│   └── sha256
│       ├── 30afc0b18f67ae8441c2d26e356693009bb8927ab7e3bce05d5ed99531c9c1d4
│       ├── 32cb805468227e4fb581624ff0d295f22b02ca102a90c5c70315b090b071701e
│       ├── 351ad75a6cfabc7f2e103963945ff803d818f0bdcf604fd2072a0eefd6674bde
│       ├── 596b1d696923618bec6ff5376cc9aed03a3724bc75b6c03221fd877b62046d05
│       ├── 69692152171afee1fd341febc390747cfca2ff302f2881d8b394e786af605696
│       ├── 8283eee92e2f756bd57f96ea295e332ab9031724267d4f939de1f7d19fe9611a
│       ├── b96e6c32a32e98ec6b0a61816b43cde674e089fe507c7a8188e2f1bb510f2373
│       └── febe5bd23e98102ed5ff64b8f5987f516a945745c08bbcf2c61a50fb6e7b2257
├── index.json
└── oci-layout

2 directories, 10 files
```

### FAQ

Error message on macOS

```bash
no image found in manifest list for architecture amd64, variant "", OS darwin
```

Solution

```bash
skopeo inspect docker://nginx --override-os linux
```

e.g.  
Pull nginx from docker hub to docker-daemon on MacOS

```bash
skopeo copy docker://docker.io/nginx --override-arch amd64 --override-os linux docker-daemon:nginx:latest
```
