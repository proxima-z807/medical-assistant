# 极简镜像：直接使用已构建好的可执行 jar（已包含前端页面与 H2 内置库）
FROM eclipse-temurin:21-jre

RUN groupadd -g 10001 medical && useradd -u 10001 -g medical -m medical
WORKDIR /app

COPY jar.part1 /app/jar.part1
COPY jar.part2 /app/jar.part2
RUN cat /app/jar.part1 /app/jar.part2 > /app/app.jar \
    && rm -f /app/jar.part1 /app/jar.part2 \
    && mkdir -p /data \
    && chown -R medical:medical /app /data

ENV APP_DATA_DIR=/data TZ=Asia/Shanghai
USER medical
EXPOSE 8080
ENTRYPOINT ["sh", "-c", "java -XX:MaxRAMPercentage=75 -Dfile.encoding=UTF-8 -jar /app/app.jar --server.port=${PORT:-8080}"]
