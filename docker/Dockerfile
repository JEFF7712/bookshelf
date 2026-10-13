FROM registry.rupan.dev/apps/dotnet-sdk-6@sha256:6115544bac6ed4ed8863e3270e088588397eec549ebe78ae8980699727c0eb94 AS toolchain
FROM registry.rupan.dev/upstream/docker.io/library/python@sha256:34386ef0cb081344d7ec1c103ba398e6e9f64e9ab3a1509accc92a4e24a07258
COPY --from=toolchain /usr/share/dotnet/dotnet /app/dotnet/dotnet
COPY --from=toolchain /usr/share/dotnet/host /app/dotnet/host
COPY --from=toolchain /usr/share/dotnet/shared /app/dotnet/shared
COPY .sovereign/build/runtime/bin /app/bin
COPY .sovereign/build/runtime/.sovereign-build.json /app/.sovereign-build.json
COPY .sovereign/base/supply/libsqlite3.so.0 /usr/lib/x86_64-linux-gnu/libsqlite3.so.0
ENV DOTNET_ROOT=/app/dotnet DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1 HOME=/tmp
USER 1000:1000
WORKDIR /app/bin
EXPOSE 8787
ENTRYPOINT ["/app/dotnet/dotnet", "/app/bin/Readarr.dll", "-nobrowser", "-data=/config"]
