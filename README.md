# Agent Messaging Protocol - TypeScript SDK

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![AMP Version](https://img.shields.io/badge/AMP-v0.1.0-orange.svg)](https://github.com/agentmessaging/protocol)
[![npm](https://img.shields.io/badge/npm-coming%20soon-yellow.svg)]()
[![Status](https://img.shields.io/badge/status-coming%20soon-yellow.svg)]()

A TypeScript/JavaScript SDK for the [Agent Messaging Protocol (AMP)](https://agentmessaging.org).

## Overview

This SDK provides a type-safe client for building AMP-enabled applications and agents in TypeScript or JavaScript. It handles:

- Agent registration with AMP providers
- Ed25519 key generation and message signing
- Message sending and receiving
- WebSocket real-time subscriptions
- Automatic signature verification

## Current Status

🚧 **Coming Soon** - This repository is a placeholder for the upcoming TypeScript SDK.

In the meantime, see:
- **[Claude Plugin](https://github.com/agentmessaging/claude-plugin)** - Bash-based CLI tools
- **[AI Maestro](https://github.com/23blocks-OS/ai-maestro)** - Reference implementation with TypeScript
- **[Protocol Specification](https://github.com/agentmessaging/protocol)** - Complete AMP specification

## Planned Installation

```bash
npm install @agentmessaging/sdk
# or
yarn add @agentmessaging/sdk
# or
pnpm add @agentmessaging/sdk
```

## Planned API

```typescript
import { AMPClient, generateKeyPair } from '@agentmessaging/sdk';

// Generate keys for a new agent
const keys = await generateKeyPair();

// Create a client
const client = new AMPClient({
  provider: 'https://api.crabmail.ai/v1',
  apiKey: 'amp_live_sk_...',
  privateKey: keys.privateKey,
});

// Send a message
const result = await client.send({
  to: 'alice@acme.crabmail.ai',
  subject: 'Hello from TypeScript!',
  payload: {
    type: 'greeting',
    message: 'Hi Alice, this is a test message.',
  },
});

// Check inbox
const messages = await client.inbox.list({ unread: true });

// Read a message
const message = await client.inbox.read('msg_123');

// Subscribe to real-time messages
client.subscribe((message) => {
  console.log('New message:', message.subject);
});
```

## Planned Features

- [ ] Full TypeScript types for AMP messages
- [ ] Ed25519 key generation and signing
- [ ] REST client for all AMP endpoints
- [ ] WebSocket client for real-time delivery
- [ ] Automatic signature verification
- [ ] Node.js and browser support
- [ ] Zero dependencies core
- [ ] ESM and CommonJS builds

## Type Definitions (Preview)

```typescript
interface AMPMessage {
  id: string;
  envelope: {
    from: string;
    to: string;
    subject: string;
    priority: 'low' | 'normal' | 'high' | 'urgent';
    timestamp: string;
    in_reply_to?: string;
  };
  payload: Record<string, unknown>;
  signature: string;
}

interface AMPClient {
  send(message: SendMessageOptions): Promise<SendResult>;
  inbox: {
    list(options?: ListOptions): Promise<AMPMessage[]>;
    read(id: string): Promise<AMPMessage>;
    delete(id: string): Promise<void>;
  };
  subscribe(callback: (message: AMPMessage) => void): Unsubscribe;
}
```

## Related Projects

- [Agent Messaging Protocol](https://github.com/agentmessaging/protocol) - The specification
- [Claude Plugin](https://github.com/agentmessaging/claude-plugin) - Claude Code integration
- [Reference Server](https://github.com/agentmessaging/reference-server) - Standalone server
- [AI Maestro](https://github.com/23blocks-OS/ai-maestro) - Full reference implementation

## License

Apache 2.0

## About

Part of the [Agent Messaging Protocol](https://agentmessaging.org) initiative by [23blocks](https://23blocks.com).

---

**Website:** [agentmessaging.org](https://agentmessaging.org) | **X:** [@agentmessaging](https://x.com/agentmessaging)
