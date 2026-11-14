FROM public.ecr.aws/docker/library/node:24.21.0-bookworm-slim@sha256:2fe369e969550cde8e867afc3fe370b260140cab4a23d467074295b42163d553

RUN set -eux; \
    apt-get -o Acquire::Retries=2 -o Acquire::http::Timeout=15 -o Acquire::https::Timeout=15 update; \
    DEBIAN_FRONTEND=noninteractive apt-get -o Acquire::Retries=2 -o Acquire::http::Timeout=15 -o Acquire::https::Timeout=15 install -y --no-install-recommends iputils-ping unzip; \
    command -v ping; ping -n -c 1 -W 1 127.0.0.1; \
    rm -rf /var/lib/apt/lists/*
WORKDIR /opt/airspace
RUN node --input-type=module -e 'import {createHash} from "node:crypto"; import {writeFile} from "node:fs/promises"; const response=await fetch("https://github.com/ckjensun-liao/HAnetbar/releases/download/v6.9.50/HA-O-Airspace-6.9.50.zip"); if(!response.ok) throw Error("Release download failed: "+response.status); const bytes=Buffer.from(await response.arrayBuffer()); if(createHash("sha256").update(bytes).digest("hex")!=="ebcf5b8c99294735a17ef10e9c36c113e0cb0eb4dbc66dcd334755630dc19bee") throw Error("Release SHA256 mismatch"); await writeFile("/tmp/airspace-release.zip",bytes);' \
    && unzip -q /tmp/airspace-release.zip -d /tmp/airspace-release \
    && cp -a /tmp/airspace-release/airspace/runtime /tmp/airspace-release/airspace/app /opt/airspace/ \
    && rm -rf /tmp/airspace-release /tmp/airspace-release.zip
ENV NODE_ENV=production
EXPOSE 8125 8100
HEALTHCHECK --interval=30s --timeout=5s --start-period=45s --retries=3 \
  CMD node -e "fetch('http://127.0.0.1:8125/healthz').then(r=>{if(!r.ok)process.exit(1)}).catch(()=>process.exit(1))"
ENTRYPOINT ["node", "/opt/airspace/runtime/index.cjs"]
