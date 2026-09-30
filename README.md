# PS5 Relapse Exploit

A modified version of the PS5 Relapse exploit with a simplified payload-loading interface and a custom visual frontend.

Supported firmware: **7.00 through 13.60**.

> This fork is currently configured around the PS5 13.60 ELF loader.

## Usage

- In the network settings, set Primary DNS to `45.56.67.85` if required for your setup.
- Run `python serve.py` locally, or open the hosted version on the PS5:
  `https://sp1kkelpoes.github.io/Relapse-Host/`
- The exploit starts automatically when the page loads.
- Wait for the WebKit and kernel stages to complete.
- After the ELF loader successfully starts on port `9021`, the **LOAD ESSENTIALS** button will appear.
- Press **LOAD ESSENTIALS** to load the included payload stack.

The payload stack is loaded in this order:

1. `kstuff.elf`
2. Wait approximately 3 seconds
3. `shadowmountplus.elf`
4. `etaHEN.elf`

The payload files are stored in `payloads/`.

## Changes in this fork

This fork is based on an older working Relapse commit and has been modified by **Sp1kkelpoes**.

Changes include:

- Restored the older payload setup.
- Added a custom payload-loading interface.
- Removed the need to press R2 to manually trigger the included payload stack.
- The payload controls only appear after the ELF loader is ready.
- Added a single **LOAD ESSENTIALS** button for the default payload sequence.
- Added status indicators and clearer exploit output.
- Added a custom dark/green interface.
- Added Matrix-style binary rain and other visual changes.
- The visual changes do not modify the underlying exploit chain.

## ELF Loader

After a successful exploit, the ELF loader listens on port:

`9021`

The included web interface uses the loader to send the default payload stack.

The ELF loader can still be used separately with compatible external payload-sending tools if desired.

## Stability Notes

The WebKit exploit may require several attempts. Reload the page if the browser stalls.

The kernel exploit may hang or panic the console. If that happens, reboot the console before attempting the exploit again.

## Exploit Chain

The browser stage uses JSC information leaks and a structured clone object pool mismatch to corrupt a TypedArray.

The kernel stage combines an address leak with an `aio_multi_wait` UAF race to establish kernel read/write access.

## Credits

Original exploit and research credits:

- ntfargo
- ufm42
- Sonic-Iso
- Jordy
- Dr. Yenyen
- TheFlow
- SlidyBat
- Flatz
- cow
- nhk
- bollarz
- Sleirsgoevy
- EchoStretch
- EarthOnion

Modified frontend and payload-loading workflow by **Sp1kkelpoes**.

## Disclaimer

This project is intended for **educational and security research purposes only**.

It does not endorse piracy, unauthorized access, or misuse of commercial devices. Use it only on devices you own or are authorized to test, and comply with applicable laws and regulations.

The software is provided as-is, without warranty. You assume the risks of using it, including system instability, data loss, and account bans. The maintainers accept no liability for resulting damage.

## About This Fork

This version restores an older Relapse configuration that worked reliably for my setup.

The original workflow required additional manual payload loading. This fork restores the required payload files and adds a simpler interface so the included payload stack can be loaded directly after the ELF loader becomes available.

The custom interface and Matrix-style visual effects are cosmetic and do not intentionally alter the underlying exploit implementation.
