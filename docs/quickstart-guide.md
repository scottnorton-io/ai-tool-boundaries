# quickstart-guide.md

# Quick Start Guide

Get your MCP security framework implementation running in under 2 hours.

## Prerequisites

- Docker and Docker Compose installed
- Basic understanding of MCP protocol
- Access to certificate authority (or use self-signed for testing)
- PostgreSQL or compatible database

## 30-Minute Proof of Concept

### Step 1: Clone and Setup (5 minutes)

```bash
# Clone the repository
git clone [https://github.com/scottnorton-io/ai-tool-boundaries.git](https://github.com/scottnorton-io/ai-tool-boundaries.git)
cd ai-tool-boundaries

# Copy example configurations
cp examples/docker-compose.example.yml docker-compose.yml
cp examples/tool-schemas/example-tools.json config/tools.json
cp examples/authorization-policies/readonly-profile.json config/policies.json
```

### Step 2: Generate Certificates (5 minutes)

```bash
# Generate CA and server certificates
./scripts/[generate-certs.sh](http://generate-certs.sh)

# Generate client certificate for test agent
./scripts/[generate-client-cert.sh](http://generate-client-cert.sh) test-agent-01
```

### Step 3: Configure Environment (5 minutes)

```bash
# Create .env file
cat > .env << EOF
MCP_GATEWAY_HOST=[localhost](http://localhost)
MCP_GATEWAY_PORT=8080
TAL_SERVICE_URL=[http://tal:8081](http://tal:8081)
AUDIT_LOG_PATH=/var/log/mcp/audit.jsonl
DB_CONNECTION_STRING=postgresql://mcp:password@db:5432/mcp
SECRET_MANAGER=vault
VAULT_ADDR=[http://vault:8200](http://vault:8200)
EOF
```

### Step 4: Start Services (5 minutes)

```bash
# Start all services
docker-compose up -d

# Verify services are running
docker-compose ps

# Check logs
docker-compose logs mcp-gateway
docker-compose logs tal-service
```

### Step 5: Test Authentication (5 minutes)

```bash
# Test client authentication
curl --cert certs/test-agent-01.crt \
     --key certs/test-agent-01.key \
     --cacert certs/ca.crt \
     [https://localhost:8080/health](https://localhost:8080/health)

# Expected response: {"status": "healthy", "version": "1.0.0"}
```

### Step 6: Test Tool Call (5 minutes)

```bash
# Make a test tool call
curl --cert certs/test-agent-01.crt \
     --key certs/test-agent-01.key \
     --cacert certs/ca.crt \
     -X POST [https://localhost:8080/tools/invoke](https://localhost:8080/tools/invoke) \
     -H "Content-Type: application/json" \
     -d '{
       "tool": "read_customer_profile",
       "parameters": {
         "customer_id": "cust_test_001"
       }
     }'

# Verify audit log entry
tail -f logs/audit.jsonl
```

## 2-Hour Production Setup

### Phase 1: Infrastructure (30 minutes)

1. **Deploy to Kubernetes:**
    
    ```bash
    kubectl apply -f examples/kubernetes/namespace.yml
    kubectl apply -f examples/kubernetes/mcp-gateway.yml
    kubectl apply -f examples/kubernetes/tal-service.yml
    ```
    
2. **Configure Network Policies:**
    
    ```bash
    kubectl apply -f examples/kubernetes/network-policies/
    ```
    
3. **Setup TLS:**
    
    ```bash
    # Use cert-manager for automated certificate management
    kubectl apply -f examples/kubernetes/cert-manager/
    ```
    

### Phase 2: Security Controls (45 minutes)

1. **Configure Tool Schemas:**
    - Review `examples/tool-schemas/` for your use case
    - Customize parameter constraints
    - Set risk classifications
    - Deploy to TAL service
2. **Setup Authorization Policies:**
    - Define client identities
    - Create tool allowlists per client
    - Configure parameter constraints
    - Test with staging clients
3. **Enable Audit Logging:**
    - Configure audit pipeline
    - Setup log aggregation (ELK, Splunk, Datadog)
    - Create retention policies
    - Test log delivery

### Phase 3: Monitoring (30 minutes)

1. **Deploy Prometheus Metrics:**
    
    ```bash
    kubectl apply -f examples/monitoring/prometheus/
    ```
    
2. **Import Grafana Dashboards:**
    - MCP Gateway metrics: `examples/monitoring/grafana/gateway-dashboard.json`
    - TAL metrics: `examples/monitoring/grafana/tal-dashboard.json`
    - Security events: `examples/monitoring/grafana/security-dashboard.json`
3. **Configure Alerts:**
    
    ```bash
    kubectl apply -f examples/monitoring/alertmanager/
    ```
    

### Phase 4: Validation (15 minutes)

1. **Run Security Tests:**
    
    ```bash
    ./scripts/[security-tests.sh](http://security-tests.sh)
    ```
    
2. **Verify Checklist:**
    - [ ]  All services healthy
    - [ ]  Certificates valid and rotating
    - [ ]  Tool schemas validated
    - [ ]  Authorization working
    - [ ]  Audit logs flowing
    - [ ]  Monitoring dashboards live
    - [ ]  Alerts configured

## Next Steps

- [ ]  Review full framework paper for advanced configurations
- [ ]  Customize tool schemas for your use cases
- [ ]  Conduct security testing
- [ ]  Train operations team on incident response
- [ ]  Schedule quarterly risk assessments

## Troubleshooting

### Authentication Failures

```bash
# Check certificate validity
openssl x509 -in certs/client.crt -text -noout

# Verify CA trust
curl --cacert certs/ca.crt [https://localhost:8080/health](https://localhost:8080/health)
```

### Tool Authorization Denials

```bash
# Check client's tool allowlist
curl --cert certs/admin.crt --key certs/admin.key \
     [https://localhost:8080/api/policies/client/test-agent-01](https://localhost:8080/api/policies/client/test-agent-01)

# Review audit logs for denial reason
grep "tool_access_denied" logs/audit.jsonl | tail -10
```

### Audit Pipeline Issues

```bash
# Verify log delivery
docker-compose logs tal-service | grep "audit_event_emitted"

# Check log aggregator connection
curl [http://localhost:9200/_cat/indices](http://localhost:9200/_cat/indices) | grep mcp-audit
```

## Support

For issues or questions:

- GitHub Issues: [https://github.com/scottnorton-io/at-tool-boundaries](https://github.com/scottnorton-io/ai-tool-boundaries)
- GitHub: [scottnorton-io](https://github.com/scottnorton-io)
- LinkedIn: [Scott Norton](https://linkedin.com/in/scottnorton-io/)