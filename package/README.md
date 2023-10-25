# yarn-npmignore-ordering

This repo contains:

```
.
├── README.md
├── index.d.ts
├── package.json
├── v1
│   ├── index.d.ts
│   └── package.json
└── yarn.lock
```

`.npmignore` is:

```
*
!**/*.d.ts
/v1/
```

Meaning, "ignore everything, unignore dts files at any level, even the root, but ignore the `v1` directory".

However, the package output is unexpected.

```console
$ yarn pack --dry-run
➤ YN0000: README.md
➤ YN0000: package.json
➤ YN0000: v1/index.d.ts
➤ YN0000: Done in 0s 12ms
```

`index.d.ts` is missing, and `v1` is included.

npm:

```console
$ COREPACK_ENABLE_STRICT=0 corepack npm@8 pack --dry-run
npm notice 
npm notice 📦  yarn-npmignore-ordering@0.0.0
npm notice === Tarball Contents === 
npm notice 441B README.md   
npm notice 30B  index.d.ts  
npm notice 96B  package.json
npm notice === Tarball Details === 
npm notice name:          yarn-npmignore-ordering                 
npm notice version:       0.0.0                                   
npm notice filename:      yarn-npmignore-ordering-0.0.0.tgz       
npm notice package size:  453 B                                   
npm notice unpacked size: 567 B                                   
npm notice shasum:        6e882b94b041dbbaa4f0654d68d8c11bd56994bb
npm notice integrity:     sha512-11HXqdIBvewZP[...]nSRa9EkPBgepg==
npm notice total files:   3                                       
npm notice 
```
