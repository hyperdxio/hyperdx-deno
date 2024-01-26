# OpenTelemetry Support for Deno

⚠️ Currently only supports OpenTelemetry Logging. For tracing support, [see the following guide](https://dev.to/grunet/leveraging-opentelemetry-in-deno-45bj#a-minimal-interesting-example).

## Logging

Logging is supported by exporting a custom logger for the `std/log` module.

**Example usage:**

```typescript
import * as log from 'https://deno.land/std@0.213.0/log/mod.ts';
import { OpenTelemetryHandler } from 'npm:@hyperdx/deno';

const otelHandler = new OpenTelemetryHandler('DEBUG');

log.setup({
  handlers: {
    otel: otelHandler,
  },

  loggers: {
    'my-otel-logger': {
      level: 'DEBUG',
      handlers: ['otel'],
    },
  },
});

log.getLogger('my-otel-logger').info('Hello from Deno!');


// OPTIONAL: Flush the logger to ensure all logs are sent to OTEL_EXPORTER_OTLP_ENDPOINT
otelHandler.flush();
```

