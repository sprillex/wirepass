# WirePass Architecture: Captive-Portal-Aware WireGuard Client

## Objective
Standard VPN tunnels ingest all outbound traffic into `tun0`. When connecting to public Wi-Fi networks behind captive portals, DNS queries and HTTP port 80 intercepts are encapsulated, causing authentication deadlocks.

WirePass solves this by orchestrating captive portal detection and isolation without disconnecting the active WireGuard tunnel.

## Key Mechanisms
1. **Dynamic Split-Tunneling:**
   - Exclude system captive portal packages (`com.google.android.captiveportallogin` and OEM equivalents) from `VpnService.Builder`.
2. **Network Callback Monitoring:**
   - Register a `ConnectivityManager.NetworkCallback` listening to `TRANSPORT_WIFI`.
   - Intercept `NET_CAPABILITY_CAPTIVE_PORTAL` and `NET_CAPABILITY_VALIDATED` states.
3. **Isolated Portal Handling:**
   - Bind HTTP resolution traffic directly to the physical Wi-Fi `Network` interface via `ConnectivityManager.bindProcessToNetwork` or `network.bindSocket` to ensure portal authorization succeeds outside the VPN tunnel.
