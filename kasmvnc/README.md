# KasmVNC

KasmVNC is a VNC server, i.e., a software used for remote control of a desktop.

## Usage

Submit the `job.kasmvnc.yaml` by using a DeepSquare client (CLI or website). The
workflow will output a bore URL in the logs. Use that URL to log in to the desktop.

Default credentials are:

- Username: `admin`
- Password: `password`

## Usage (holepunch)

Holepunch is a solution for UDP holepunching. You need to use a local proxy to divert traffic from the DHT network.

1. Install [hyperproxy](https://github.com/deepsquare-io/hyperproxy). It is not published as a NPM package, so use the Git URL:

   ```shell
   pnpm install -g git+https://github.com/deepsquare-io/hyperproxy.git
   # or
   npm install -g git+https://github.com/deepsquare-io/hyperproxy.git
   ```

2. Install `hyper-cmd-utils` and generate a key:

   ```shell
   pnpm install -g hyper-cmd-utils
   # or
   npm install -g hyper-cmd-utils

   hyper-cmd-util-keygen --gen_seed
   ```

3. Edit `job.kasmvnc.holepunch.yaml` and replace the seed.

4. Submit `job.kasmvnc.holepunch.yaml` with the DeepSquare Portal or CLI. An address will be given in the logs.

5. Open the client proxy by using the address:

   ```shell
   hyperproxy -s <address>
   ```
