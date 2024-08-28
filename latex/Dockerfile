FROM pandoc/latex
# USER
ARG MY_USER_ID=1000
ARG MY_USER_NAME=nonroot
ARG MY_GROUP_ID=1000
ARG MY_GROUP_NAME=nonroot
RUN addgroup -g $MY_GROUP_ID $MY_GROUP_NAME && adduser -u $MY_USER_ID -G $MY_GROUP_NAME -s /bin/ash -D $MY_USER_NAME && mkdir -p /workdir && chown -R $MY_USER_ID:$MY_GROUP_ID /workdir
USER $MY_USER_NAME
ENTRYPOINT [ "sleep", "infinity" ]
