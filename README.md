# API Gateway

Simple, YAML-based API Gateway with virtual hosts, route management, and consumer authentication.

## Core Features

- Virtual host support
- Flexible route matching (path, method, headers)
- Consumer authentication and rate limiting
- Dynamic failover for upstream services
- Header transformation
- SSL/TLS support
- CORS configuration

## Configuration Structure

```yaml
api_gateway/
  ├── virtual_hosts/           # Domain configurations
  │   ├── hostname            
  │   ├── default_settings    # Global virtual host settings
  │   └── routes/            # Path-based routing rules
  └── api_consumers/         # API client definitions
```

## Route Selection Process

1. Match virtual host
2. Match path
3. Match HTTP method
4. Validate API consumer
5. Check routing headers
6. Forward to upstream service

## Failover Behavior

The gateway automatically fails over to backup services when:
- Primary service is unreachable
- Request times out (configurable timeout)
- Maximum retries reached

## Example Usage

Minimal configuration:
```yaml
api_gateway:
  virtual_hosts:
    - hostname: api.example.com
      routes:
        - path: /api
          methods: [GET]
          upstream_config:
            strategy: direct
            services:
              - url: http://backend:8080
  
  api_consumers:
    - name: client
      key: api-key-123
      status: active
```

## Security Considerations

- Always use HTTPS in production
- Rotate API keys regularly
- Set appropriate rate limits
- Use strong passwords for basic auth
- Configure CORS carefully

## Limitations

- No dynamic routing rules
- No caching layer
- No request/response transformation
- No circuit breaker
- No service discovery integration
