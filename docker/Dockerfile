FROM bitwalker/alpine-elixir-phoenix:1.14 AS builder

WORKDIR /app

COPY ../dev.env ./.env

RUN apk --no-cache --update add alpine-sdk gmp-dev automake libtool inotify-tools autoconf python3 file qemu-x86_64  
RUN export $(cat ./.env | xargs) 
    

ENV GLIBC_REPO=https://github.com/sgerrand/alpine-pkg-glibc \
    GLIBC_VERSION=2.30-r0 \
    PORT=4000 \
    MIX_ENV="prod" \
    SECRET_KEY_BASE="RMgI4C1HSkxsEjdhtGMfwAHfyT6CKWXOgzCboJflfSm4jeAlic52io05KB6mqzc5" \
    COIN="" \
    CACHE_EXCHANGE_RATES_PERIOD="" \
    API_V1_READ_METHODS_DISABLED="false" \
    DISABLE_WEBAPP="false" \
    API_V1_WRITE_METHODS_DISABLED="false" \
    CACHE_TOTAL_GAS_USAGE_COUNTER_ENABLED="" \
    CACHE_ADDRESS_WITH_BALANCES_UPDATE_INTERVAL="" \
    ADMIN_PANEL_ENABLED="" \
    RELEASE_VERSION=5.1.4 \
    ETHEREUM_JSONRPC_VARIANT=geth \


    ETHEREUM_JSONRPC_HTTP_URL=http://localhost:8000 \
    ETHEREUM_JSONRPC_TRACE_URL=http://localhost:8000 \
    DATABASE_URL=postgresql://postgres:postgres123@db:5432/blockscan?ssl=false \

    NETWORK=Axon \
    SUBNETWORK=AxonChain \
    LOGO=/images/blockscout_logo.svg \
    LOGO_FOOTER=/images/blockscout_logo.svg \
    ETHEREUM_JSONRPC_TRANSPORT=http \
    IPC_PATH= \
    NETWORK_PATH=/  \
    API_PATH=/  \
    SOCKET_ROOT=/ \
    BLOCKSCOUT_HOST= \
    BLOCKSCOUT_PROTOCOL= \
    PORT=4020 \
    EMISSION_FORMAT=DEFAULT \
    POOL_SIZE=40 \
    POOL_SIZE_API=10 \
    ECTO_USE_SSL=false \
    HEART_BEAT_TIMEOUT=30 \
    BLOCKSCOUT_VERSION= \
    RELEASE_LINK= \
    BLOCK_TRANSFORMER=axon \
    LINK_TO_OTHER_EXPLORERS=false \
    OTHER_EXPLORERS={} \
    SUPPORTED_CHAINS={} \
    CACHE_BLOCK_COUNT_PERIOD=7200 \
    CACHE_TXS_COUNT_PERIOD=7200 \
    CACHE_ADDRESS_COUNT_PERIOD=7200 \
    CACHE_ADDRESS_SUM_PERIOD=3600 \
    CACHE_TOTAL_GAS_USAGE_PERIOD=3600 \
    CACHE_ADDRESS_TRANSACTIONS_GAS_USAGE_COUNTER_PERIOD=1800 \
    CACHE_TOKEN_HOLDERS_COUNTER_PERIOD=3600 \
    CACHE_TOKEN_TRANSFERS_COUNTER_PERIOD=3600 \
    CACHE_ADDRESS_WITH_BALANCES_UPDATE_INTERVAL=1800 \
    CACHE_AVERAGE_BLOCK_PERIOD=1800 \
    CACHE_MARKET_HISTORY_PERIOD=21600 \
    CACHE_ADDRESS_TRANSACTIONS_PERIOD=1800 \
    CACHE_ADDRESS_TOKENS_USD_SUM_PERIOD=1800 \
    CACHE_ADDRESS_TOKEN_TRANSFERS_COUNTER_PERIOD=1800 \
    CACHE_BRIDGE_MARKET_CAP_UPDATE_INTERVAL=1800 \
    CACHE_TOKEN_EXCHANGE_RATE_PERIOD=1800 \
    TOKEN_METADATA_UPDATE_INTERVAL=172800 \
    ALLOWED_EVM_VERSIONS=homestead,tangerineWhistle,spuriousDragon,byzantium,constantinople,petersburg,istanbul,berlin,london,default \
    UNCLES_IN_AVERAGE_BLOCK_TIME=false \
    DISABLE_WEBAPP=false \
    DISABLE_READ_API=false \
    DISABLE_WRITE_API=false \
    DISABLE_INDEXER=false
    INDEXER_DISABLE_PENDING_TRANSACTIONS_FETCHER=true \
    INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER=true \
    WOBSERVER_ENABLED=false \
    SHOW_ADDRESS_MARKETCAP_PERCENTAGE=true \
    CHECKSUM_ADDRESS_HASHES=true \
    CHECKSUM_FUNCTION=eth \
    DISABLE_EXCHANGE_RATES=true \
    DISABLE_KNOWN_TOKENS=true \
    ENABLE_TXS_STATS=true \
    SHOW_PRICE_CHART=false \
    SHOW_TXS_CHART=true \
    HISTORY_FETCH_INTERVAL=30 \
    TXS_HISTORIAN_INIT_LAG=0 \
    TXS_STATS_DAYS_TO_COMPILE_AT_INIT=10 \
    COIN_BALANCE_HISTORY_DAYS=90 \
    APPS_MENU=true \
    EXTERNAL_APPS=[] \
    DISABLE_BRIDGE_MARKET_CAP_UPDATER=true \
    INDEXER_DISABLE_BLOCK_REWARD_FETCHER=true \
    ENABLE_POS_STAKING_IN_MENU=false \
    SHOW_MAINTENANCE_ALERT=false \
    MAINTENANCE_ALERT_MESSAGE= \
    SHOW_STAKING_WARNING=false \
    STAKING_WARNING_MESSAGE= \
    CUSTOM_CONTRACT_ADDRESSES_TEST_TOKEN= \
    ENABLE_SOURCIFY_INTEGRATION=false \
    SOURCIFY_SERVER_URL= \
    SOURCIFY_REPO_URL= \
    MAX_SIZE_UNLESS_HIDE_ARRAY=50 \
    HIDE_BLOCK_MINER=false \
    DISPLAY_TOKEN_ICONS=false \
    SHOW_TENDERLY_LINK=false \
    TENDERLY_CHAIN_PATH= \
    MAX_STRING_LENGTH_WITHOUT_TRIMMING=2040 \
    RE_CAPTCHA_SECRET_KEY= \
    RE_CAPTCHA_CLIENT_KEY= \
    API_RATE_LIMIT=50 \
    API_RATE_LIMIT_BY_KEY=50 \
    API_RATE_LIMIT_BY_IP=50 \ 
    API_RATE_LIMIT_WHITELISTED_IPS= \
    API_RATE_LIMIT_STATIC_API_KEY=
    



RUN set -ex && \
    apk --update add libstdc++ curl ca-certificates && \
    for pkg in glibc-${GLIBC_VERSION} glibc-bin-${GLIBC_VERSION}; \
        do curl -sSL ${GLIBC_REPO}/releases/download/${GLIBC_VERSION}/${pkg}.apk -o /tmp/${pkg}.apk; done && \
    apk add --allow-untrusted /tmp/*.apk && \
    rm -v /tmp/*.apk && \
    /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib

# Get Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

ENV PATH="$HOME/.cargo/bin:${PATH}"
ENV RUSTFLAGS="-C target-feature=-crt-static"

ARG CACHE_EXCHANGE_RATES_PERIOD
ARG DISABLE_READ_API
ARG DISABLE_WEBAPP
ARG DISABLE_WRITE_API
ARG CACHE_TOTAL_GAS_USAGE_COUNTER_ENABLED
ARG ADMIN_PANEL_ENABLED
ARG CACHE_ADDRESS_WITH_BALANCES_UPDATE_INTERVAL
ARG SESSION_COOKIE_DOMAIN
ARG MIXPANEL_TOKEN
ARG MIXPANEL_URL
ARG AMPLITUDE_API_KEY
ARG AMPLITUDE_URL

# Cache elixir deps
ADD mix.exs mix.lock ./
ADD apps/block_scout_web/mix.exs ./apps/block_scout_web/
ADD apps/explorer/mix.exs ./apps/explorer/
ADD apps/ethereum_jsonrpc/mix.exs ./apps/ethereum_jsonrpc/
ADD apps/indexer/mix.exs ./apps/indexer/

RUN mix do deps.get, local.rebar --force, deps.compile

ADD . .

COPY . .

# Run forderground build and phoenix digest
RUN mix compile && npm install npm@latest

# Add blockscout npm deps
RUN cd apps/block_scout_web/assets/ && \
    npm install && \
    npm run deploy && \
    cd /app/apps/explorer/ && \
    npm install && \
    apk update && \
    apk del --force-broken-world alpine-sdk gmp-dev automake libtool inotify-tools autoconf python3

RUN mix phx.digest

RUN mkdir -p /opt/release \
  && mix release blockscout \
  && mv _build/${MIX_ENV}/rel/blockscout /opt/release

##############################################################
FROM bitwalker/alpine-elixir-phoenix:1.14

ARG RELEASE_VERSION
ENV RELEASE_VERSION=${RELEASE_VERSION}
ARG BLOCKSCOUT_VERSION
ENV BLOCKSCOUT_VERSION=${BLOCKSCOUT_VERSION}

RUN apk --no-cache --update add jq

WORKDIR /app

COPY --from=builder /opt/release/blockscout .
COPY --from=builder /app/apps/explorer/node_modules ./node_modules
COPY --from=builder /app/config/config_helper.exs ./config/config_helper.exs
COPY --from=builder /app/config/config_helper.exs /app/releases/${RELEASE_VERSION}/config_helper.exs

