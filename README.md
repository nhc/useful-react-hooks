# useful-react-hooks

Some hooks. Most to be used with AWS

## useAgentInvoke

1. Setup an Agent in AWS Bedrock.
2. Create and Alias
3. Get the id for both

Use it like this

```typescript
import { BedrockAgentRuntimeClient } from "@aws-sdk/client-bedrock-agent-runtime";

const bedrockClient = new BedrockAgentRuntimeClient({
  region: "us-east-1",
  credentials: {
    accessKeyId: import.meta.env.VITE_AWSACCESSKEY,
    secretAccessKey: import.meta.env.VITE_AWSSECRETKEY,
  },
});

const YourComponent = () => {
  const { invokeAgent, isLoading, error } = useAgentInvoke({
    agentId: "xxxxxxxx",
    agentAliasId: "xxxxxx",
    sessionId: "your-session-id", // this will persist the AI session between requests
    bedrockClient: yourBedrockClient,
  });

  const handleInvoke = async () => {
    const result = await invokeAgent("Your prompt");
    if (result) {
      // Handle the result
    }
  };

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return <button onClick={handleInvoke}>Invoke Agent</button>;
};
```
