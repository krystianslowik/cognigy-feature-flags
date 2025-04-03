# Feature Flags and Configuration Settings

This document provides a comprehensive overview of all feature flags and configuration settings available in the Cognigy platform. It serves as a reference for support engineers.

## Table Structure
- **Feature Flag/Setting Name**: The name of the flag as it appears in configuration files
- **Description**: Explanation of what the feature flag controls
- **Team Responsible**: Team responsible for maintaining this feature
- **Hard Limit**: Maximum allowed value 
- **Soft Limit**: Recommended maximum value 
- **Default Value**: Default setting if not explicitly configured
- **Notes**: Additional information, warnings, or usage recommendations

## Using This Document

This document is organized into sections based on functional areas of the platform. Each section contains tables of related configuration settings.

# Primary Settings
## Core Feature Flags

| Feature Flag/Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:--------------------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `knowledgeSearch.enabled` | Temporary flag for the "Knowledge Search" feature. Controls whether the Knowledge Search functionality is available. | | | | `false` | Please DO NOT use this flag for now if you are a customer running Cognigy.AI/Cognigy Insights using this HelmChart. |
| `knowledgeSearch.globalAzureDocumentIntelligenceConfig.enabled` | Controls whether the system-wide Azure AI Document Intelligence configuration is enabled. Only takes effect when the parent 'knowledgeSearch' feature is enabled. | | | | `false` | |
| `platformProvidedLLM.whitelist` | Comma-separated list of organization IDs that are allowed to use the platform provided LLM. `["*"]` for all organizations. Leave as empty list to disable the feature. | | | | `[]` | |
| `platformProvidedLLM.provider` | The LLM provider to use. Currently supported: `"azureOpenAI"` | | | | `"azureOpenAI"` | |
| `platformProvidedLLM.model` | The LLM model to use. Currently supported: `"gpt-4o"`, `"gpt-4o-mini"` | | | | `"gpt-4o-mini"` | |
| `cognigyAgentAssist.enabled` | Set to true to enable Agent Assist Workspace | | | | `false` | |
| `cognigyAgentAssist.enableGenesysNotificationsForwarder` | Set it to true to use the Genesys Notification Forwarder | | | | `false` | |
| `FEATURE_DISABLE_RESET_FLOW` | Disables the "resetting of flow" functionality when set to `"true"` | | | | `"true"` | |
| `FEATURE_REDIS_SENTINEL_MODE_ENABLED` | Enable Redis Sentinel (HA mode) | | | | `"true"` | |
| `FEATURE_REDIS_PERSISTENT_SENTINEL_MODE_ENABLED` | Enable Redis Persistent Sentinel (HA mode) | | | | `"true"` | |
| `FEATURE_CUSTOM_NODES` | Controls whether custom nodes are enabled | | | | `"true"` | |
| `FEATURE_USE_SERVICE_INSIGHTS_UI` | Enable new Cognigy Insights UI | | | | `"true"` | |
| `FEATURE_INSIGHTS_USE_CONVERSATIONS_DELETION` | Enable conversations deletion in Insights | | | | `"true"` | |
| `FEATURE_ENABLE_HANDOVER_SETTINGS_FOR_VG2` | Enable Handover settings in the VG2 Endpoint | | | | `"true"` | |
| `FEATURE_INSIGHTS_USE_CUBE_JS_FILTERS_PREAGGREGATIONS` | Enable using Cube.js filters preaggregations | | | | `"false"` | |
| `FEATURE_INSIGHTS_USE_CUBE_JS_MESSAGES_PREAGGREGATIONS` | Enable using Cube.js messages preaggregations | | | | `"false"` | |
| `FEATURE_ALLOW_ADDITIONAL_ACTIONS_IN_CODE_NODES` | Controls whether additional actions are allowed in code nodes | | | | `"false"` (commented) | Extra security measure for code nodes |
| `FEATURE_USE_COGNIGY_DOC_LINKS` | Enables links to Cognigy documentation | | | | Not set (commented) | |
| `FEATURE_USE_WHITELABELING` | Allows customers to white-label the platform | | | | Not set (commented) | Replaces Cognigy.AI with a generic name when enabled |
| `FEATURE_ALLOW_TRUSTED_CODE_CONFIGURATION` | Enables updating the 'trustedCode' property of extensions | | | | Not set (commented) | Security-related setting |
| `FEATURE_USE_GENESYS_CLOUD` | Enables Genesys Cloud handover provider | | | | Not set (commented) | |
| `FEATURE_LICENSE_AGREEMENT` | Controls whether users need to accept a license agreement | | | | Not set (commented) | |
| `FEATURE_APIKEY_AUTH` | Enables API key authentication | | | | Not set (commented) | |
| `FEATURE_ENABLE_FOLLOW_SESSION` | Enables the "Follow Sessions" feature | | | | Not set (commented) | |
| `FEATURE_USE_SOCKETENDPOINT_EVENTBUFFER` | Enables assured message delivery for socketendpoint | | | | Not set (commented) | |
| `FEATURE_DISABLE_SERVICE_NLP_MATCHER` | Disables service NLP matcher except for specified orgs | | | | Not set (commented) | |

## System Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `MESSAGE_TTL_SECONDS` | The TTL of messages in the endpoint-session-queues in seconds | | | | `"120"` | |
| `MAX_MEMORY_OBJECT_SIZE` | Maximum memory object size for context, profiles, etc. (in bytes) | | | | `"65536"` (64 KB) | Can be increased in dedicated environments, but may lead to performance issues |
| `HTTP_JSON_BODY_LIMIT` | Maximum JSON body size for HTTP requests (in bytes) | | | | `"65536"` (64 KB) | |
| `MAX_BYTE_SIZE` | Maximum byte size for general operations (in bytes) | | | | `"524288"` (512 KB) | |
| `RESPONSE_BYTES_LIMIT` | Maximum HTTP response size (in bytes) | | | | `"524288"` (512 KB) | Default is 512 KB, 2.6 MB in Trial, 1.5 MB in App |
| `HTTP_NODE_TIMEOUT_IN_SECONDS` | Timeout for HTTP requests in the httpRequest Node (in seconds) | | | | `"30"` (8s default, 15s in App) | |
| `LOG_ENTRIES_TTL_IN_MINUTES` | How long log entries are kept (in minutes) | | | | `"1440"` | Default is 24 hours |
| `LOG_ENTRIES_BUFFER_IN_SECONDS` | Buffer time for log entries before writing (in seconds) | | | | `"5"` | |
| `MODULE_MAX_EVENT_EMISSIONS` | Maximum number of event emissions from modules | | | | `"10"` | |
| `MAX_MODULE_EXECUTION_TIME_IN_SECONDS` | Maximum execution time for modules (in seconds) | | | | `"20"` | |
| `MAX_CONTACT_PROFILE_TTL_IN_MINUTES` | Maximum TTL for contact profiles (in minutes) | | | | `"43200"` | Default is 30 days |
| `MAX_CONVERSATION_TTL_IN_MINUTES` | Maximum TTL for conversations (in minutes) | | | | `"43200"` | Default is 30 days |
| `MAX_SESSION_STATE_TTL_IN_MINUTES` | Maximum TTL for session states (in minutes) | | | | `"10080"` | Default is 7 days |
| `CUBEJS_SCHEDULED_REFRESH_CONCURRENCY` | Maximum number of concurrent pre-aggregation refreshes | | | | `"10"` | |
| `AI_LRU_CACHE_CHART_EXECUTABLE_ENABLED` | Enables chart executable caching | | | | Not set (commented) | |
| `AI_LRU_CACHE_CHART_EXECUTABLE_MAX_SIZE` | Maximum number of chart executables in cache | | | | Not set (commented) | |
| `AI_LRU_CACHE_CHART_EXECUTABLE_MAX_AGE_IN_SECONDS` | Maximum age of chart executables in cache (in seconds) | | | | Not set (commented) | |
| `AI_LRU_CACHE_PROJECT_ENABLED` | Enables project caching | | | | Not set (commented) | |
| `AI_LRU_CACHE_PROJECT_MAX_SIZE` | Maximum number of projects in cache | | | | Not set (commented) | |
| `AI_LRU_CACHE_PROJECT_MAX_AGE_IN_SECONDS` | Maximum age of projects in cache (in seconds) | | | | Not set (commented) | |
| `AI_LRU_CACHE_CONNECTION_ENABLED` | Enables connection caching | | | | Not set (commented) | |
| `AI_LRU_CACHE_CONNECTION_MAX_SIZE` | Maximum number of connections in cache | | | | Not set (commented) | |
| `AI_LRU_CACHE_CONNECTION_MAX_AGE_IN_SECONDS` | Maximum age of connections in cache (in seconds) | | | | Not set (commented) | |
| `AI_BRAIN_TTL` | TTL for AI brains (in ms) | | | | `"600000"` | 10 minutes |
| `AI_BRAIN_CLEANUP_INTERVAL` | Cleanup interval for AI brains (in ms) | | | | `"60000"` | 1 minute |
| `AI_FLOW_CACHE_MAX_SIZE` | Maximum number of flows in cache | | | | Not set (commented) | |
| `AI_FLOW_CACHE_TTL_IN_SEC` | TTL for flows in cache (in seconds) | | | | Not set (commented) | |
| `AI_SESSION_STATE_CACHE_CLEANUP_INTERVAL_IN_SEC` | Cleanup interval for session state cache (in seconds) | | | | Not set (commented) | |
| `AI_SESSION_STATE_CACHE_TTL_IN_SEC` | TTL for session state in cache (in seconds) | | | | Not set (commented) | |
| `AI_SESSION_STATE_CACHE_MAX_COUNT_PER_CLEANUP_CYCLE` | Maximum items to clean up per cycle | | | | Not set (commented) | |
| `MAX_AMOUNT_OF_OPERATIONS_PER_BATCH_CALL` | Maximum operations per batch call | | | | `"10"` | |
| `NLP_MAX_MATCHER_LEN` | Maximum length for exact matching | | | | `"50"` | |
| `MAX_EXTENSIONS_CACHE_DIR_SIZE_IN_MB` | Maximum size for extensions cache directory (in MB) | | | | `"1024"` | 1 GB |
| `EXECUTE_EXTENSIONS_IN_VM` | Controls whether extensions are executed in a VM | | | | `"true"` | Security feature |
| `FUNCTION_EXECUTION_MAX_EXECUTION_TIME_IN_MINUTES` | Maximum time a function instance can run (in minutes) | | | | `"60"` | Default is 60 min (1 hour), 15 min in quotas doc |
| `FUNCTION_INSTANCE_MAX_RUNNING_NUMBER_PER_ORGANIZATION` | Maximum concurrent function instances per organization | | | | `"10"` | |
| `MAX_CONCURRENT_PLAYBOOK_EXECUTIONS` | Maximum concurrent playbook executions | | | | `"25"` | Default is 25, 10 in quotas doc |
| `RUNTIME_FILE_MANAGER_MAX_FILE_SIZE` | Maximum file size for runtime files (in bytes) | | | | `"10485760"` | 10 MB |
| `SECURITY_ACCESS_TOKEN_LENGTH` | Length of access tokens | | | | `"48"` | |
| `SECURITY_REFRESH_TOKEN_LENGTH` | Length of refresh tokens | | | | `"64"` | |
| `REFRESH_TOKEN_MAX_AMOUNT_PER_USER` | Maximum refresh tokens per user | | | | `"5"` | |
| `API_ACCESS_TOKEN_EXPIRATION_IN_MINUTES` | Access token lifetime (in minutes) | | | | `"60"` | 1 hour |
| `API_REFRESH_TOKEN_SHORT_EXPIRATION_IN_MINUTES` | Short-lived refresh token lifetime (in minutes) | | | | `"1440"` | 1 day |
| `API_REFRESH_TOKEN_LONG_EXPIRATION_IN_MINUTES` | Long-lived refresh token lifetime (in minutes) | | | | `"10080"` | 7 days |
| `SOCKET_ENDPOINT_DISCONNECT_GRACE_PERIOD` | Waiting period before the user disconnected event is triggered (in seconds) | | | | `"3"` | Can be changed in dedicated environments |

## Agent Assist Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `cognigyAgentAssist.enabled` | Enable Agent Assist Workspace | | | | `false` | |
| `cognigyAgentAssist.enableGenesysNotificationsForwarder` | Enable Genesys Notification Forwarder | | | | `false` | |
| `cognigyAgentAssist.accessToken` | Access token for Agent Assist Workspace API | | | | `""` | |
| `FEATURE_ENABLE_AGENT_ASSIST_WORKSPACE_WHITELIST` | Enable Agent Assist Workspace whitelist | | | | Not set | |
| `FEATURE_ENABLE_AGENT_ASSIST_WORKSPACE_GENESYS_CREDENTIALS_WHITELIST` | Enable Agent Assist Workspace Genesys credentials whitelist | | | | Not set | |

# Secondary Configuration (Additional Settings)

## Integration Settings

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `WEBCHAT_EMBEDDER_WHITELIST` | Controls which origins can embed the webchat iframe | | | | Not set (commented) | Use `"*"` to allow all domains |
| `WEBCHAT_FORCE_WEBSOCKETS` | Force webchat to use websockets instead of polling | | | | `"false"` (commented) | |
| `ALLOWED_EXTENSION_HOSTNAMES` | Controls allowed hosts for remote extension loading | | | | `"github.com,localhost"` | Security feature |
| `FRONTEND_BASE_URL_WITH_PROTOCOL` | Override URL for frontend | | | | `""` | Useful for custom domains |
| `BACKEND_BASE_URL_WITH_PROTOCOL` | Override URL for backend API | | | | `""` | Useful for custom domains |
| `API_BASE_URL_WITH_PROTOCOL` | Override URL for API | | | | `""` | Useful for custom domains |
| `WEBCHAT_ENDPOINT_BASE_URL_WITH_PROTOCOL` | Override URL for webchat endpoint | | | | `""` | Useful for custom domains |
| `VOICE_GATEWAY_ENDPOINT_URL` | URL for voice gateway endpoint | | | | `""` | |
| `VG_WEBAPP_ACCESS_WHITELIST` | Controls org access to VG WebApp | | | | `""` | Use `"*"` for all orgs |
| `EMAIL_NOTIFICATION_FROM` | From address for email notifications | | | | `"noreply@cognigy.com"` | |
| `EMAIL_NOTIFICATION_SUBJECT_PREFIX` | Subject prefix for email notifications | | | | `"[Cognigy]"` | |
| `CONNECTION_FIELDS_ENCRYPTION_KEY` | Encryption key for connection fields | | | | Random value | 32-character key |
| `DISABLE_LICENSE_UPLOAD` | Disables license installation routes for cloud installations | | | | `"false"` | |
| `SESSION_SECRET` | Used for OpenID Connect implementation | | | | Random value | 32-character string |

## MongoDB Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `mongodb.enabled` | Controls whether MongoDB connection and initialization is enabled | | | | `true` | Set to false if neither Cognigy MongoDB Helm Chart nor MongoDB Atlas is used |
| `mongodb.scheme` | MongoDB connection scheme | | | | `"mongodb"` | For MongoDB Atlas use `"mongodb+srv"` |
| `mongodb.params` | Parameters for MongoDB connection | | | | `""` | For MongoDB Atlas set params: `"?retryWrites=true&w=majority"` |
| `mongodb.auth.rootUser` | MongoDB admin username | | | | `"root"` | This user must have permission to create users and databases |
| `mongodb.hosts` | MongoDB connection string | | | | `"mongodb-0.mongodb-headless.mongodb.svc.cluster.local:27017,mongodb-1.mongodb-headless.mongodb.svc.cluster.local:27017,mongodb-2.mongodb-headless.mongodb.svc.cluster.local:27017"` | |
| `dbConnectionString.enabled` | Controls whether to generate MongoDB connection strings | | | | `true` | |
| `INSIGHTS_DBINIT_INDEX_CREATION_DISABLE` | Disable index creation for insights db in DB_INIT migration | | | | `"true"` | |

## Voice Gateway & Call Settings

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `ALEXA_END_SESSION_AFTER_EACH_REPLY` | Whether to end Alexa session after each reply | | | | `"true"` | |
| `FEATURE_ENABLE_HANDOVER_SETTINGS_FOR_VG2` | Enable handover settings in VG2 Endpoint | | | | `"true"` | |
| `cognigyVoicegatewayClientSecret.token` | Client secret for Voice Gateway integration | | | | Random 64 character string | Should match client secret in VG cluster |
| `VG_WEBAPP_ACCESS_WHITELIST` | Whitelist of OrgIDs for VG WebApp access | | | | Not set | Use `"*"` for all OrgIDs |

## Management UI Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `managementUi.enabled` | Install Management UI on the cluster | | | | `false` | Not required if API endpoint is accessible from internet |
| `managementUi.ingress.enabled` | Enable ingress for Management UI | | | | `true` | |
| `managementUi.image` | Management UI Docker image | | | | `"cognigy.azurecr.io/management-ui:release-bfcc652906-1742991638"` | |
| `managementUi.replicaCount` | Number of Management UI replicas | | | | `1` | |
| `managementUiCredentials` | Credentials for Management UI | | | | `"[]"` | JSON array of username/password objects |

## Security & Authentication

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `commonSecrets.cognigyJwt.token` | JWT secret for signing tokens | | | | Random 128 character string | Used for realtime tokens |
| `commonSecrets.cognigyOauthClientSecret.token` | OAuth Client Secret | | | | Random 64 character string | |
| `commonSecrets.cognigyServiceEndpointApiAccessToken.token` | Service Endpoint API access token | | | | Random 16 character string | |
| `commonSecrets.cognigyServiceHandoverApiAccessToken.token` | Service Handover API access token | | | | Random 16 character string | |
| `commonSecrets.cognigySearchOrchestratorApiKey.token` | Search Orchestrator API key | | | | Random 16 character string | |
| `commonSecrets.cognigySecureFormsApiKey.token` | Secure Forms API key | | | | `""` | |
| `OAUTH_CLIENT_ID` | OAuth client ID | | | | `"cognigy-ui"` | |
| `CLIENT_ID_COGNIGY_VOICE_GATEWAY` | Voice Gateway client ID | | | | `"voicegateway"` | |
| `CLIENT_ID_COGNIGY_LIVE_AGENT` | Live Agent client ID | | | | `"cognigy-live-agent"` | |

## Cognitive Services Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `knowledgeSearch.globalAzureDocumentIntelligenceConfig.apiKey` | Azure Document Intelligence API key | | | | `""` | |
| `knowledgeSearch.globalAzureDocumentIntelligenceConfig.endpointUrl` | Azure Document Intelligence endpoint URL | | | | `""` | |
| `platformProvidedLLM.azure.resourceName` | Azure OpenAI resource name | | | | `""` | |
| `platformProvidedLLM.azure.deploymentName` | Azure OpenAI deployment name | | | | `""` | |
| `platformProvidedLLM.azure.apiVersion` | Azure OpenAI API version | | | | `""` | |
| `platformProvidedLLM.azure.credentials.apiKey` | Azure OpenAI API key | | | | `""` | |
| `NLP_PRECOMPUTED_EMBEDDINGS_PATH` | Path to files with pre-computed noise embeddings | | | | `"/embedding/precomputed_embeddings"` | |

## Live Agent Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `cognigyLiveAgent.platformToken` | API token for Live Agent | | | | Random 24 character string | |
| `FEATURE_USE_COGNIGY_LIVE_AGENT` | Activate Cognigy Live Agent | | | | Not set | |
| `CLIENT_SECRET_COGNIGY_LIVE_AGENT` | Client secret for Live Agent | | | | Not set | |
| `REDIRECT_URI_COGNIGY_LIVE_AGENT` | Redirect URI for Live Agent | | | | Not set | |
| `CLIENT_ID_COGNIGY_LIVE_AGENT` | Client ID for Live Agent | | | | Not set | |
| `LIVE_AGENT_BACKEND_BASE_URL_WITH_PROTOCOL` | Base URL for Live Agent backend | | | | Not set | |
| `LIVE_AGENT_API_CORS_WHITELIST` | CORS whitelist for Live Agent API | | | | Not set | |
| `LIVE_AGENT_API_SECRET` | Live Agent API secret | | | | Not set | |
| `LIVE_AGENT_TOKEN_TTL_IN_SECONDS` | TTL for Live Agent JWT and access token | | | | Not set | |
| `FEATURE_USE_COGNIGY_LIVE_AGENT_DASHBOARD` | Activate Live Agent Dashboard | | | | Not set | |

## Monitoring & Metrics

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `MONITOR_RPC_CALLS` | Enable metrics collection for RPC calls | | | | `"true"` | Consumed by service-monitoring |
| `FEATURE_RPC_LOGS` | Enable detailed logs for RPC calls handling | | | | Not set | |
| `RPC_TIMEOUT_GET_NLU_RESULTS_IN_MS` | Timeout for 'getNluResultsRpc' call | | | | `"5000"` | |
| `CREATE_RUNTIME_FILE_TIMEOUT_IN_SECONDS` | RPC timeout for creating runtime file in seconds | | | | Not set | Default is 8 seconds |

## Network Rate Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `API Rate Limit` | Maximum number of requests from a single IP address | | | | `1000 requests per 5 minutes` | Applies only to shared SaaS environments |

## NLU and Training Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `Maximum Example Sentences per Intent` | Number of example sentences allowed for a single Intent | | | | `200` | |
| `Maximum Total Example Sentences` | Total number of example sentences across all Intents including Attached Flows | | | | `10,000` (`15,000` in Trial) | |
| `Maximum Total Intents` | Total number of Intents across all Flows including Attached Flows | | | | `2,500` (`10,000` in Trial) | |
| `Maximum Intent Training Time` | Maximum time an Intent-Training task is allowed to run | | | | `10 minutes` | |
| `Maximum Intent Trainer Upload Size` | Maximum file size for uploading Intent Trainer records | | | | `100 MB` | |
| `Maximum Intent Trainer Record Storage` | Maximum time Intent Trainer records are stored | | | | `10 days` | |

## Flow Execution and Code Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `Maximum Code Execution Time` | Maximum execution time in Code Node | | | | `1 second` | |
| `Maximum Character Count in Code Editor` | Maximum number of characters in the code editor | | | | `200,000` | |
| `Maximum API Calls per Code Node` | Maximum number of API calls from a single Code Node | | | | `100` | |
| `Maximum Flow Loop Protection` | Maximum number of times a Flow can execute the same Path for a single user message | | | | `4` | Before "Infinite Loop protection" is triggered |
| `Maximum Undo/Redo Operations` | Maximum number of undo/redo operations stored per user in Flow Editor | | | | `5` | |

## Transformer Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `Maximum Transformer HTTP Requests` | Maximum number of HTTP requests from a Transformer | | | | `1` (`2` in Trial) | |
| `Maximum Transformer Execution Time` | Maximum execution time for a Transformer | | | | `5 seconds` | |

## Email (SMTP Node) Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| `Maximum Email Retry Attempts` | Maximum number of times the system retries to send an outbound Email | | | | `3` | |
| `Maximum Email Attachment Size` | Maximum size of an Email attachment | | | | `10 MB` | |

## Data Retention Periods

| Description | Default Value | Notes |
|:------------|:--------------|:-------|
| Log-Line retention | `1 day` | Maximum time until a Log-Line on the product's Log page will be removed |
| Flow-execution session retention | `30 days` | Maximum time until relevant Flow-execution session information will be removed |
| Contact Profile retention | `30 days` | Maximum time until a Contact Profile which has not been read or modified will be removed |
| Conversation transcript retention | `30 days` | Maximum time until Conversation transcripts will be removed |
| Intent Trainer record retention | `10 days` | Maximum time Intent Trainer records are stored in the database |
| Audit event retention | `30 days` | Maximum time until audit events will be removed |
| xApp Session retention | `30 days` | Maximum time until an xApp Session will be expired |
| PCAP File retention (Voice Gateway) | `14 days` | Maximum time until a PCAP File will be removed |

## Internal notes

## primary settings 

1. **feature flag changes** – always test in staging before prod. don’t skip validation.
2. **system limits** – changing these can affect performance + stability. monitor after applying.
3. **agent assist** – controls agent assist behavior + genesys integration. only adjust if you know what you're doing.
4. **security settings** – options like EXECUTE_EXTENSIONS_IN_VM, FEATURE_ALLOW_ADDITIONAL_ACTIONS_IN_CODE_NODES, and FEATURE_ALLOW_TRUSTED_CODE_CONFIGURATION are critical. evaluate all changes carefully.
5. **performance tuning** – settings like AI_LRU_CACHE_* and TTL values impact performance directly.

## additional settings

6. **mongodb config** – wrong connection settings can break things. handle with care.
7. **auth settings** – never commit secrets. never log them.
8. **knowledge search** – feature is still in development. don’t enable for customers.
9. **platform llm config** – double-check model + provider settings when enabling.
10. **integration urls** – if using custom domains, make sure all related urls are set correctly.
11. **token security** – token lifetime settings affect both security and user experience.

## environment-specific variations

12. **trial & app envs** – some limits are different here. check reference tables.
13. **dedicated saas** – limits can be adjusted for customers on dedicated environments if requested.
---

*Note: This documentation is based on the current configuration as of April 2025. Feature flags and settings may change with new releases.*
