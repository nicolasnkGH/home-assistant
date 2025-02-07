# 🌐 Access Home Assistant Remotely via Cloudflare Tunnel

This guide will walk you through the steps required to securely access your Home Assistant instance remotely using Cloudflare Tunnel. You'll need a domain (either paid or free) to complete the setup.

## 🔧 Prerequisites:
- A domain name (can be a paid or free domain).
- Home Assistant running on your local network.
- Cloudflare account and Cloudflare Tunnel setup.
- Setting up Cloudflare Tunnel https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/

## 🛠️ How to Set Up:

### 1. **Prepare Your Domain with Cloudflare:**
   - Sign up for a Cloudflare account if you don't have one.
   - If your domain is not provided by CloudFlare, you can transfer it. To transfer your domain to Cloudflare. See https://developers.cloudflare.com/registrar/get-started/transfer-domain-to-cloudflare/

### 2. **Update Home Assistant Configuration:**
   - Open your `configuration.yaml` file located in your Home Assistant configuration folder.
   - Add the following configuration under:

   ```yaml
   # Cloudflare remote access
http:
  # Enable support for the X-Forwarded-For header to track the original IP address of requests.
  use_x_forwarded_for: true

  # Define trusted proxies. This ensures that only requests coming from the specified IP range are allowed.
  # This IP range is typically used by the Cloudflare Tunnel add-on.
  trusted_proxies:
    - 172.30.33.0/24  # The IP range used by the Cloudflare Tunnel to securely forward traffic to your Home Assistant instance

```


### 3. Install Cloudflare Add-On in Home Assistant:
1. Go to **Add-ons** > **Add-on Store** in Home Assistant.
2. Click on the three dots menu (top-right corner) and select **Repositories** > **Add New**.
3. Paste the following URL into the repository field:

   ```text
   https://github.com/brenner-tobias/ha-addons
   ```
4. Once added, search for the Cloudflare Tunnel add-on and click Install.

 ### 4. Configure the Cloudflare Add-On:
1. Go to **Configurations** within the **Cloudflare Tunnel** add-on.
2. Add your external domain in the **External Domain** field.

   **Tip:** It's recommended to create a subdomain for this purpose (e.g., `hahome.example.net`). This allows automatic identification on Cloudflare tunnels and provides a clean URL for accessing Home Assistant externally.

   ![image](https://github.com/user-attachments/assets/0616d816-c440-479b-bec5-32ccb035d1a0)


4. **Save** the configuration.

### 5. Start the Cloudflare Tunnel Add-On:
1. After saving the configuration, return to the add-on page and click **Start** to start the Cloudflare Tunnel add-on.
2. Check the logs for a generated URL.
3. Copy the provided URL and paste it into your browser to authorize the Cloudflare Tunnel.

### 6. Access Home Assistant Remotely:
Once the Cloudflare Tunnel is authorized, your Home Assistant instance will be accessible from your external domain (e.g., `https://hahome.example.net`).

Enjoy secure remote access to your Home Assistant instance!

## 🔒 Security Considerations:
- **HTTPS:** Ensure your Cloudflare Tunnel is using HTTPS to secure the connection.
- **Authentication:** Set up authentication methods for your Home Assistant instance (e.g., long-lived access tokens) to restrict unauthorized access.
- **Firewalls & Restrictions:** Make sure to configure your firewall to only allow access to the necessary ports and services.

## ⚖️ Legal Disclaimer:
By following these steps, you agree to comply with all applicable laws and regulations regarding remote access and the use of Home Assistant. The repository creator is not responsible for any misuse or security breaches.
  
   
