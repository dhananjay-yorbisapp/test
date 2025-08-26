# Nium vs Monex API Comparison

## Complete URL Mapping

| Category | Nium URL | Monex URL |
|----------|----------|-----------|
| Onboarding (corporate) | https://api.spend.nium.com/api/v1/client/{clientId}/corporate | https://sbox.monexusa.com/api/onboard |
| Add Beneficiary | https://api.spend.nium.com/api/v2/client/{clientId}/customer/{customerId}/beneficiaries | https://sbox.monexusa.com/api/beneficiaries |
| Get Beneficiaries | https://api.spend.nium.com/api/v2/client/{clientId}/customer/{customerId}/beneficiaries | https://sbox.monexusa.com/api/beneficiaries |
| Get Wallets | https://api.spend.nium.com/api/v1/client/{clientId}/customer/{customerId}/wallet/{walletID} | https://sbox.monexusa.com/api/wallets |
| Get Wallet Details | https://api.spend.nium.com/api/v1/client/{clientId}/customer/{customerId}/wallet/{walletID} | https://sbox.monexusa.com/api/wallet/{walletID} |
| Fund Wallet | https://api.spend.nium.com/api/v1/client/{clientId}/customer/{customerId}/wallet/{walletID}/fund | https://sbox.monexusa.com/api/transactions |
| Transfer Money | https://api.spend.nium.com/api/v1/client/{clientId}/customer/{customerId}/wallet/{walletID}/remittance | https://sbox.monexusa.com/api/transactions |
| FX Quote | https://api.spend.nium.com/api/v1/client/{clientId}/quotes | https://sbox.monexusa.com/api/quotes |
| FX Conversion | https://api.spend.nium.com/api/v1/client/{clientId}/customer/{customerId}/wallet/{walletHashID}/conversions | https://sbox.monexusa.com/api/transactions/convert |
| Purpose Codes | https://api.spend.nium.com/api/v1/remittance/purposeCodes | https://sbox.monexusa.com/api/reference/purposeCodes |
| Get Payees | https://api.spend.nium.com/api/v2/client/{clientId}/customer/{customerId}/beneficiaries | https://sbox.monexusa.com/api/beneficiaries |
| Delete Payee | https://api.spend.nium.com/api/v1/client/{clientId}/customer/{customerId}/beneficiaries/{beneficiaryhashID} | https://sbox.monexusa.com/api/beneficiaries/{beneficiaryHashID} |

## Authentication Comparison

### Nium Authentication
- **Method**: API Key + Client ID in headers
- **Headers**: 
  - `X-API-KEY: ${NIUM_API_KEY}`
  - `X-CLIENT-ID: ${NIUM_CLIENT_ID}`

### Monex Authentication
- **Method**: Bearer token (JWT) obtained via `/auth`
- **Headers**: 
  - `Authorization: Bearer {{token}}`
- **Auth Endpoint**: `https://sbox.monexusa.com/api/auth`

## Implementation Notes

1. **URL Patterns**: Nium uses nested resource URLs with client ID, customer ID, and wallet ID, while Monex uses simpler resource-based URLs.

2. **Authentication**: Monex requires initial authentication to obtain JWT token, while Nium uses static API keys.

3. **Versioning**: Nium explicitly versions endpoints (v1, v2), while Monex uses implicit versioning.

4. **Placeholder Parameters**:
   - Nium: `{clientId}`, `{customerId}`, `{walletID}`, `{walletHashID}`, `{beneficiaryhashID}`
   - Monex: `{walletID}`, `{beneficiaryHashID}`

## Configuration Template

```properties
# Provider Selection
payment.provider=NIUM  # or MONEX

# Nium Configuration
nium.base-url=https://api.spend.nium.com
nium.client-id=${NIUM_CLIENT_ID}
nium.api-key=${NIUM_API_KEY}

# Monex Configuration
monex.base-url=https://sbox.monexusa.com/api
monex.public-key=${MONEX_PUBLIC_KEY}
monex.secret-key=${MONEX_SECRET_KEY}
```
