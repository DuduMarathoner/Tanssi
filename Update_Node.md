### Check log node
```
docker logs -f tanssi
```
## Update Node
```
docker stop tanssi
docker rm tanssi
docker pull moondancelabs/tanssi
```
- Please change `TANSSI_NAME` to your name

```
docker run --name tanssi --network="host" -d -v "$HOME/dancebox:/data" \
-u $(id -u ${USER}):$(id -g ${USER}) \
moondancelabs/tanssi \
--chain=dancebox \
--name=TANSSI_NAME \
--sync=warp \
--base-path=/data/para \
--state-pruning=2000 \
--blocks-pruning=2000 \
--collator \
--telemetry-url='wss://telemetry.polkadot.io/submit/ 0' \
--database paritydb \
-- \
--name=TANSSI_NAME \
--base-path=/data/container \
--telemetry-url='wss://telemetry.polkadot.io/submit/ 0' \
-- \
--chain=westend_moonbase_relay_testnet \
--name=TANSSI_NAME \
--sync=fast \
--base-path=/data/relay \
--state-pruning=2000 \
--blocks-pruning=2000 \
--telemetry-url='wss://telemetry.polkadot.io/submit/ 0' \
--database paritydb
docker update --restart=unless-stopped tanssi
```
