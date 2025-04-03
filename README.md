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

## Environment Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| global.imageRegistry | Global Docker image registry for Cognigy images | | | | "" | |
| cloud.provider | Cloud provider type | | | | "aws" | Options: "aws", "azure", "generic" (for on-premises) |
| cloud.region | Cloud provider region | | | | "" | |
| imageCredentials.registry | Private registry URL | | | | "cognigy.azurecr.io" | |
| imageCredentials.username | Registry username | | | | "" | |
| imageCredentials.password | Registry password | | | | "" | |
| imageCredentials.pullSecrets | Array of image pull secrets | | | | [] | Alternative to username/password |

## Core Feature Flags

| Feature Flag/Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:--------------------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| knowledgeSearch.enabled | Temporary flag for the "Knowledge Search" feature. Controls whether the Knowledge Search functionality is available. | | | | false | Please DO NOT use this flag for now if you are a customer running Cognigy.AI/Cognigy Insights using this HelmChart. |
| knowledgeSearch.globalAzureDocumentIntelligenceConfig.enabled | Controls whether the system-wide Azure AI Document Intelligence configuration is enabled. Only takes effect when the parent 'knowledgeSearch' feature is enabled. | | | | false | |
| platformProvidedLLM.whitelist | Comma-separated list of organization IDs that are allowed to use the platform provided LLM. ["*"] for all organizations. Leave as empty list to disable the feature. | | | | [] | |
| platformProvidedLLM.provider | The LLM provider to use. Currently supported: "azureOpenAI" | | | | "azureOpenAI" | |
| platformProvidedLLM.model | The LLM model to use. Currently supported: "gpt-4o", "gpt-4o-mini" | | | | "gpt-4o-mini" | |
| cognigyAgentAssist.enabled | Set to true to enable Agent Assist Workspace | | | | false | |
| cognigyAgentAssist.enableGenesysNotificationsForwarder | Set it to true to use the Genesys Notification Forwarder | | | | false | |
| FEATURE_DISABLE_RESET_FLOW | Disables the "resetting of flow" functionality when set to "true" | | | | "true" | |
| FEATURE_REDIS_SENTINEL_MODE_ENABLED | Enable Redis Sentinel (HA mode) | | | | "true" | |
| FEATURE_REDIS_PERSISTENT_SENTINEL_MODE_ENABLED | Enable Redis Persistent Sentinel (HA mode) | | | | "true" | |
| FEATURE_CUSTOM_NODES | Controls whether custom nodes are enabled | | | | "true" | |
| FEATURE_USE_SERVICE_INSIGHTS_UI | Enable new Cognigy Insights UI | | | | "true" | |
| FEATURE_INSIGHTS_USE_CONVERSATIONS_DELETION | Enable conversations deletion in Insights | | | | "true" | |
| FEATURE_ENABLE_HANDOVER_SETTINGS_FOR_VG2 | Enable Handover settings in the VG2 Endpoint | | | | "true" | |
| FEATURE_INSIGHTS_USE_CUBE_JS_FILTERS_PREAGGREGATIONS | Enable using Cube.js filters preaggregations | | | | "false" | |
| FEATURE_INSIGHTS_USE_CUBE_JS_MESSAGES_PREAGGREGATIONS | Enable using Cube.js messages preaggregations | | | | "false" | |

## System Limits

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| MESSAGE_TTL_SECONDS | The TTL of messages in the endpoint-session-queues in seconds | | | | "120" | |
| MAX_MEMORY_OBJECT_SIZE | Maximum memory object size for context, profiles, etc. (in bytes) | | | | "65536" | |
| HTTP_JSON_BODY_LIMIT | Maximum JSON body size for HTTP requests (in bytes) | | | | "65536" | |
| MAX_BYTE_SIZE | Maximum byte size for general operations (in bytes) | | | | "524288" | |
| RESPONSE_BYTES_LIMIT | Maximum response size (in bytes) | | | | "524288" | |
| LOG_ENTRIES_TTL_IN_MINUTES | How long log entries are kept (in minutes) | | | | "1440" | Default is 24 hours |
| LOG_ENTRIES_BUFFER_IN_SECONDS | Buffer time for log entries before writing (in seconds) | | | | "5" | |
| MODULE_MAX_EVENT_EMISSIONS | Maximum number of event emissions from modules | | | | "10" | |
| MAX_MODULE_EXECUTION_TIME_IN_SECONDS | Maximum execution time for modules (in seconds) | | | | "20" | |
| MAX_CONTACT_PROFILE_TTL_IN_MINUTES | Maximum TTL for contact profiles (in minutes) | | | | "43200" | Default is 30 days |
| MAX_CONVERSATION_TTL_IN_MINUTES | Maximum TTL for conversations (in minutes) | | | | "43200" | Default is 30 days |
| MAX_SESSION_STATE_TTL_IN_MINUTES | Maximum TTL for session states (in minutes) | | | | "10080" | Default is 7 days |
| CUBEJS_SCHEDULED_REFRESH_CONCURRENCY | Maximum number of concurrent pre-aggregation refreshes | | | | "10" | |

## MongoDB Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| mongodb.enabled | Controls whether MongoDB connection and initialization is enabled | | | | true | Set to false if neither Cognigy MongoDB Helm Chart nor MongoDB Atlas is used |
| mongodb.scheme | MongoDB connection scheme | | | | "mongodb" | For MongoDB Atlas use "mongodb+srv" |
| mongodb.params | Parameters for MongoDB connection | | | | "" | For MongoDB Atlas set params: "?retryWrites=true&w=majority" |
| mongodb.auth.rootUser | MongoDB admin username | | | | "root" | This user must have permission to create users and databases |
| mongodb.hosts | MongoDB connection string | | | | "mongodb-0.mongodb-headless.mongodb.svc.cluster.local:27017,mongodb-1.mongodb-headless.mongodb.svc.cluster.local:27017,mongodb-2.mongodb-headless.mongodb.svc.cluster.local:27017" | |
| dbConnectionString.enabled | Controls whether to generate MongoDB connection strings | | | | true | |
| INSIGHTS_DBINIT_INDEX_CREATION_DISABLE | Disable index creation for insights db in DB_INIT migration | | | | "true" | |

### MongoDB Service Connection Configuration

Each service can have its own MongoDB connection configuration:

| Service Name | Enabled by Default | Service Connection Name | Notes |
|:-------------|:-------------------|:------------------------|:-------|
| serviceAi | true | service-ai | |
| serviceAlexaManagement | true | service-alexa-management | |
| serviceAnalyticsCollector | true | service-analytics-collector | |
| serviceAnalyticsConversations | true | service-analytics-conversation | |
| serviceApi | true | service-api | |
| serviceAppSessionManager | true | service-app-session-manager | |
| serviceCollaboration | false | service-collaboration | Part of new functionality |
| serviceSentinel | false | service-sentinel | Part of new functionality |
| serviceCustomModules | true | service-custom-modules | |
| serviceFunctionScheduler | true | service-function-scheduler | |
| serviceHandover | true | service-handover | |
| serviceHandoverInactivity | true | service-handover-inactivity | |
| serviceInsightsResources | false | service-insights-resources | |
| serviceLogs | true | service-logs | |
| serviceNlp | true | service-nlp | |
| serviceProfiles | true | service-profiles | |
| serviceResources | true | service-resources | |
| serviceRuntimeFileManager | true | service-runtime-file-manager | |
| serviceSecurity | true | service-security | |
| serviceTaskManager | true | service-task-manager | |
| serviceTrainer | true | service-trainer | |
| agentAssistBackend | true | agent-assist | |

## Voice Gateway & Call Settings

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| ALEXA_END_SESSION_AFTER_EACH_REPLY | Whether to end Alexa session after each reply | | | | "true" | |
| FEATURE_ENABLE_HANDOVER_SETTINGS_FOR_VG2 | Enable handover settings in VG2 Endpoint | | | | "true" | |
| cognigyVoicegatewayClientSecret.token | Client secret for Voice Gateway integration | | | | Random 64 character string | Should match client secret in VG cluster |
| VG_WEBAPP_ACCESS_WHITELIST | Whitelist of OrgIDs for VG WebApp access | | | | Not set | Use * for all OrgIDs |

## Agent Assist Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| cognigyAgentAssist.enabled | Enable Agent Assist Workspace | | | | false | |
| cognigyAgentAssist.enableGenesysNotificationsForwarder | Enable Genesys Notification Forwarder | | | | false | |
| cognigyAgentAssist.accessToken | Access token for Agent Assist Workspace API | | | | "" | |
| FEATURE_ENABLE_AGENT_ASSIST_WORKSPACE_WHITELIST | Enable Agent Assist Workspace whitelist | | | | Not set | |
| FEATURE_ENABLE_AGENT_ASSIST_WORKSPACE_GENESYS_CREDENTIALS_WHITELIST | Enable Agent Assist Workspace Genesys credentials whitelist | | | | Not set | |

## Management UI Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| managementUi.enabled | Install Management UI on the cluster | | | | false | Not required if API endpoint is accessible from internet |
| managementUi.ingress.enabled | Enable ingress for Management UI | | | | true | |
| managementUi.image | Management UI Docker image | | | | "cognigy.azurecr.io/management-ui:release-bfcc652906-1742991638" | |
| managementUi.replicaCount | Number of Management UI replicas | | | | 1 | |
| managementUiCredentials | Credentials for Management UI | | | | "[]" | JSON array of username/password objects |

## Security & Authentication

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| commonSecrets.cognigyJwt.token | JWT secret for signing tokens | | | | Random 128 character string | Used for realtime tokens |
| commonSecrets.cognigyOauthClientSecret.token | OAuth Client Secret | | | | Random 64 character string | |
| commonSecrets.cognigyServiceEndpointApiAccessToken.token | Service Endpoint API access token | | | | Random 16 character string | |
| commonSecrets.cognigyServiceHandoverApiAccessToken.token | Service Handover API access token | | | | Random 16 character string | |
| commonSecrets.cognigySearchOrchestratorApiKey.token | Search Orchestrator API key | | | | Random 16 character string | |
| commonSecrets.cognigySecureFormsApiKey.token | Secure Forms API key | | | | "" | |
| OAUTH_CLIENT_ID | OAuth client ID | | | | "cognigy-ui" | |
| CLIENT_ID_COGNIGY_VOICE_GATEWAY | Voice Gateway client ID | | | | "voicegateway" | |
| CLIENT_ID_COGNIGY_LIVE_AGENT | Live Agent client ID | | | | "cognigy-live-agent" | |

## Cognitive Services Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| knowledgeSearch.globalAzureDocumentIntelligenceConfig.apiKey | Azure Document Intelligence API key | | | | "" | |
| knowledgeSearch.globalAzureDocumentIntelligenceConfig.endpointUrl | Azure Document Intelligence endpoint URL | | | | "" | |
| platformProvidedLLM.azure.resourceName | Azure OpenAI resource name | | | | "" | |
| platformProvidedLLM.azure.deploymentName | Azure OpenAI deployment name | | | | "" | |
| platformProvidedLLM.azure.apiVersion | Azure OpenAI API version | | | | "" | |
| platformProvidedLLM.azure.credentials.apiKey | Azure OpenAI API key | | | | "" | |
| NLP_PRECOMPUTED_EMBEDDINGS_PATH | Path to files with pre-computed noise embeddings | | | | "/embedding/precomputed_embeddings" | |

## Email Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| smtpPassword | Password for SMTP server | | | | "" | For "forgot password" functionality |
| smtpOAuth2.auth.clientId | Client ID for email OAuth2 | | | | "" | |
| smtpOAuth2.auth.clientSecret | Client secret for email OAuth2 | | | | "" | |
| smtpOAuth2.auth.refreshToken | Refresh token for email OAuth2 | | | | "" | |
| smtpOAuth2.auth.accessToken | Access token for email OAuth2 | | | | "" | |
| smtpEmailNotificationCredentials.authType | Authentication type for email notifications | | | | "basic" | Options: "basic" or "oauth2" |
| SYSTEM_SMTP_HOST | SMTP server hostname | | | | "test" | |
| SYSTEM_SMTP_PORT | SMTP server port | | | | "test" | |
| SYSTEM_SMTP_USERNAME | SMTP server username | | | | "test" | |
| SYSTEM_SMTP_FROM | SMTP from address | | | | "test" | |
| SYSTEM_SMTP_CONNECTION_TYPE | SMTP connection type | | | | "starttls" | |

## Live Agent Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| cognigyLiveAgent.platformToken | API token for Live Agent | | | | Random 24 character string | |
| FEATURE_USE_COGNIGY_LIVE_AGENT | Activate Cognigy Live Agent | | | | Not set | |
| CLIENT_SECRET_COGNIGY_LIVE_AGENT | Client secret for Live Agent | | | | Not set | |
| REDIRECT_URI_COGNIGY_LIVE_AGENT | Redirect URI for Live Agent | | | | Not set | |
| CLIENT_ID_COGNIGY_LIVE_AGENT | Client ID for Live Agent | | | | Not set | |
| LIVE_AGENT_BACKEND_BASE_URL_WITH_PROTOCOL | Base URL for Live Agent backend | | | | Not set | |
| LIVE_AGENT_API_CORS_WHITELIST | CORS whitelist for Live Agent API | | | | Not set | |
| LIVE_AGENT_API_SECRET | Live Agent API secret | | | | Not set | |
| LIVE_AGENT_TOKEN_TTL_IN_SECONDS | TTL for Live Agent JWT and access token | | | | Not set | |
| FEATURE_USE_COGNIGY_LIVE_AGENT_DASHBOARD | Activate Live Agent Dashboard | | | | Not set | |

## Monitoring & Metrics

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| MONITOR_RPC_CALLS | Enable metrics collection for RPC calls | | | | "true" | Consumed by service-monitoring |
| FEATURE_RPC_LOGS | Enable detailed logs for RPC calls handling | | | | Not set | |
| RPC_TIMEOUT_GET_NLU_RESULTS_IN_MS | Timeout for 'getNluResultsRpc' call | | | | "5000" | |
| CREATE_RUNTIME_FILE_TIMEOUT_IN_SECONDS | RPC timeout for creating runtime file in seconds | | | | Not set | Default is 8 seconds |

## Deployment & Infrastructure Configuration

### Horizontal Pod Autoscaler (HPA)

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| hpa.enabled | Enable HPA globally | | | | false | Experimental feature, not recommended for production use |
| hpa.removeReplicas | When true, remove replicas field from deployment manifests | | | | true | Used when HPA is enabled |
| hpa.useHpaTolerations | Add tolerations to HPA-managed services | | | | true | |
| hpa.useHpaNodeSelector | Add nodeSelector to HPA-managed services | | | | true | |
| hpa.hpaTolerations[0].key | Toleration key for HPA nodes | | | | "node-role.cognigy.ai" | |
| hpa.hpaTolerations[0].value | Toleration value for HPA nodes | | | | "autoscaler" | |
| hpa.hpaTolerations[0].effect | Toleration effect for HPA nodes | | | | "NoSchedule" | |

### Service-specific HPA Configuration

These settings can be configured for each individual service that supports HPA:

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| horizontalPodAutoscaler.enabled | Enable horizontal pod autoscaler for specific service | | | | false | Overrides global setting |
| horizontalPodAutoscaler.minReplicas | Minimum number of replicas to scale down to | | | | 3 | |
| horizontalPodAutoscaler.maxReplicas | Maximum number of replicas to scale up to | | | | 30 | |
| horizontalPodAutoscaler.metrics[0].resource.name | Resource metric to monitor for scaling | | | | "cpu" | |
| horizontalPodAutoscaler.metrics[0].resource.target.averageUtilization | CPU utilization threshold to trigger scaling | | | | 70 | |
| horizontalPodAutoscaler.behavior | Scaling behavior configuration | | | | {} | Can be used to fine-tune scaling behavior |

## Service Configuration

| Service Name | Default Replica Count | CPU Request | Memory Request | CPU Limit | Memory Limit | Notes |
|:-------------|:---------------------|:------------|:---------------|:-----------|:------------|:-------|
| serviceAi | 3 | 0.4 | 400M | 0.4 | 500M | |
| serviceAlexaManagement | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceAnalyticsCollector | 3 | 0.3 | 160M | 0.3 | 200M | |
| serviceAnalyticsConversations | 3 | 0.1 | 120M | 0.3 | 250M | |
| serviceAnalyticsOdata | 3 | 0.1 | 360M | 0.5 | 450M | |
| serviceAnalyticsReporter | 3 | 0.5 | 500M | 0.5 | 750M | |
| serviceApi | 3 | 0.2 | 400M | 0.4 | 700M | |
| serviceAppSessionManager | 3 | 0.4 | 400M | 0.4 | 500M | |
| serviceCollaboration | 3 | 0.3 | 512M | 0.3 | 512M | Disabled by default (enabled: false). Part of new functionality that's actively being developed. |
| serviceSentinel | 3 | 0.3 | 512M | 0.3 | 512M | Disabled by default (enabled: false). Part of new functionality that's actively being developed. |
| serviceCustomModules | 3 | 0.3 | 512M | 0.3 | 512M | |
| serviceEndpoint | 3 | 0.2 | 300M | 0.3 | 300M | |
| serviceExecution | 3 | 1.0 | 240M | 1.0 | 300M | Can be configured with horizontal pod autoscaler |
| serviceFunctionExecution | 3 | 1.0 | 512M | 2.0 | 512M | Can be configured with horizontal pod autoscaler |
| serviceFunctionScheduler | 3 | 0.1 | 60M | 0.3 | 150M | Can be configured with horizontal pod autoscaler |
| serviceHandover | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceHandoverInactivity | 3 | 0.1 | 150M | 0.4 | 150M | Enabled by default (enabled: true). Can be configured with horizontal pod autoscaler |
| serviceHttp | 3 | 0.1 | 60M | 0.1 | 75M | Can be configured with horizontal pod autoscaler |
| serviceInsightsApi | 3 | 0.1 | 100M | 0.3 | 200M | |
| serviceInsightsResources | 3 | 0.1 | 100M | 0.3 | 200M | Disabled by default (enabled: false) |
| serviceInsightsForwarder | 3 | 0.1 | 100M | 0.3 | 200M | Disabled by default (enabled: false) |
| serviceCollector | 3 | 0.1 | 128M | 0.5 | 256M | |
| serviceInsightsUi | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceLogs | 3 | 0.1 | 100M | 0.5 | 150M | |
| serviceNlpMatcher | 3 | 0.2 | 300M | 0.5 | 500M | |
| serviceNlpNer | 3 | 0.3 | 100M | 1.0 | 150M | Can be configured with horizontal pod autoscaler |
| serviceParser | 3 | 0.1 | 60M | 0.3 | 150M | |
| servicePlaybookExecution | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceProfiles | 3 | 0.1 | 60M | 0.3 | 150M | Can be configured with horizontal pod autoscaler |
| serviceResources | 3 | 0.2 | 512M | 1.0 | 1Gi | |
| serviceRuntimeFileManager | 3 | 0.4 | 400M | 0.4 | 500M | Can be configured with horizontal pod autoscaler |
| serviceSecurity | 3 | 0.2 | 60M | 0.4 | 150M | |
| serviceSessionStateManager | 3 | 0.4 | 400M | 0.4 | 500M | Can be configured with horizontal pod autoscaler |
| serviceStaticFiles | 3 | 0.4 | 400M | 0.4 | 500M | |
| serviceTaskManager | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceTrainer | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceUi | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceWebchat | 3 | 0.1 | 60M | 0.3 | 150M | |
| serviceSearchOrchestrator | 3 | 0.3 | 500M | 1.0 | 1.0G | |
| agentAssistBackend | 3 | 400m | 400Mi | 600m | 600Mi | For Agent Assist functionality |
| agentAssistFrontend | 3 | 400m | 400Mi | 600m | 600Mi | For Agent Assist functionality |
| agentAssistGenesysNotificationsForwarder | 3 | 400m | 400Mi | 600m | 600Mi | For Genesys integration |

## NLP Services

These services are disabled by default and can be enabled based on language needs.

| Service Name | Enabled by Default | Replica Count | CPU Request | Memory Request | CPU Limit | Memory Limit | Description |
|:-------------|:-------------------|:--------------|:------------|:---------------|:-----------|:------------|:-------------|
| serviceNlpEmbeddingEn | false | 2 | 0.3 | 2Gi | 0.4 | 3Gi | English embedding service |
| serviceNlpEmbeddingXx | false | 2 | 0.4 | 1.2Gi | 0.8 | 2Gi | Multilingual embedding service |
| serviceNlpEmbeddingGe | false | 2 | 0.3 | 3Gi | 1.0 | 4Gi | Generic embedding service |
| serviceNlpClassifierScoreEn | false | 2 | 0.3 | 350M | 1.0 | 750M | English classifier for scoring |
| serviceNlpClassifierTrainEn | false | 2 | 0.3 | 300M | 1.0 | 1000M | English classifier for training |
| serviceNlpOrchestrator | false | 2 | 0.3 | 700M | 1.0 | 1200M | NLP orchestration service |
| serviceNlpClassifierScoreGe | false | 2 | 0.3 | 1G | 1.0 | 2G | Generic classifier for scoring |
| serviceNlpClassifierTrainGe | false | 2 | 0.3 | 1G | 1.0 | 2G | Generic classifier for training |
| serviceNlpClassifierScoreDe | false | 2 | 0.3 | 150M | 1.0 | 500M | German classifier for scoring |
| serviceNlpClassifierTrainDe | false | 2 | 0.3 | 300M | 1.0 | 1000M | German classifier for training |
| serviceNlpClassifierScoreJa | false | 2 | 0.3 | 150M | 1.0 | 500M | Japanese classifier for scoring |
| serviceNlpClassifierTrainJa | false | 2 | 0.3 | 300M | 1.0 | 1000M | Japanese classifier for training |
| serviceNlpClassifierScoreKo | false | 2 | 0.3 | 150M | 1.0 | 500M | Korean classifier for scoring |
| serviceNlpClassifierTrainKo | false | 2 | 0.3 | 300M | 1.0 | 1000M | Korean classifier for training |
| serviceNlpClassifierScoreXx | false | 2 | 0.3 | 1G | 1.0 | 2G | Multilingual classifier for scoring |
| serviceNlpClassifierTrainXx | false | 2 | 0.3 | 1G | 1.0 | 2G | Multilingual classifier for training |

### NLP Service Configuration

| Setting Name | Description | Default Value | Notes |
|:-------------|:-------------|:--------------|:-------|
| livenessProbe.failureThreshold | Number of failures before considering pod failed | 1 | Used in training services |
| livenessProbe.initialDelaySeconds | Initial delay before first probe | 120 | Allows time for model loading |
| livenessProbe.periodSeconds | Interval between probes | 60 | |
| livenessProbe.timeoutSeconds | Timeout for probe response | 60 | |

## Scheduled Jobs

| Job Name | Schedule | CPU Request | Memory Request | CPU Limit | Memory Limit | Description | Notes |
|:----------|:---------|:------------|:---------------|:-----------|:------------|:-------------|:-------|
| jobDailyConversationReporter | 0 1 * * * (daily at 1 AM) | 0.2 | 60M | 0.4 | 150M | Daily job to generate conversation reports | Uses service-security container image |
| jobSyncKnowledgeData | 0 1 * * * (daily at 1 AM) | 0.3 | 150M | 0.5 | 300M | Syncs data between MongoDB and vector database | Disabled by default (enabled: false) |
| cronNfsCleanup | 0 * * * * (hourly) | 0.1 | 60M | 0.3 | 150M | Cleans up NFS snapshots and packages | Removes snapshots/packages older than defined age |
| cronNfsCleanupTranscripts | 3 * * * * (hourly at minute 3) | 0.1 | 30M | 0.2 | 60M | Cleans up transcript files | |
| insightsDataCleanupJob | */10 * * * * (every 10 minutes) | 0.3 | 150M | 0.5 | 300M | Deletes leftover data from MongoDB | Enabled by default |
| jobCopyNfs | On-demand | 0.4 | 500M | 1.0 | 1G | Copies Functions/Extensions from NFS | Disabled by default (enabled: false) |
| migration.endpointDeletion | On-demand | N/A | N/A | N/A | N/A | Removes sunsetted/retired endpoints | Disabled by default (enabled: false) |

## Knowledge Processing Tasks

These tasks handle knowledge data for semantic search functionality.

| Task Name | CPU Request | Memory Request | CPU Limit | Memory Limit | Timeout | Description |
|:-----------|:------------|:---------------|:-----------|:------------|:---------|:-------------|
| taskProcessKnowledgeSourceFile | 0.1 | 200M | 0.3 | 1000M | 15 min | Processes knowledge source files |
| taskProcessKnowledgeSourceUrl | 0.1 | 512M | 0.3 | 750M | 15 min | Processes knowledge source URLs |
| taskIngestKnowledgeChunks | 0.1 | 60M | 0.3 | 200M | 15 min | Ingests knowledge chunks into vector store |
| taskCreatePackageNfs | 1.0 | 1Gi | 1.5 | 2Gi | 120 min | Creates packages on NFS storage |
| unstructuredIo | 0.1 | 512M | 0.3 | 750M | N/A | Standalone service for document processing |

### Job Configuration Parameters

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| successfulJobsHistoryLimit | Number of successful job executions to keep | | | | 3 | For audit and troubleshooting |
| failedJobsHistoryLimit | Number of failed job executions to keep | | | | 3 | For audit and troubleshooting |
| jobActiveDeadlineSeconds | Time before Kubernetes terminates a running job | | | | 86400 (24 hours) | Cleanup timing for killed jobs |
| jobTtlSecondsAfterFinished | Time to keep job data after finish | | | | 3600 (60 minutes) | Cleanup timing for completed jobs |
| activeDeadlineSeconds | Maximum runtime for the job | | | | 7200 (2 hours) | Prevents jobs from running indefinitely |
| ttlSecondsAfterFinished | Time to keep job information | | | | 86400 (24 hours) | Keep job information for 1 day |

## Storage & Persistence Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| flowModules.persistence.aws.efs.enabled | Enable AWS EFS for flow modules storage | | | | true | For AWS cloud provider only |
| flowModules.persistence.aws.efs.id | EFS filesystem ID for flow modules | | | | "" | Required when EFS is enabled |
| flowModules.persistence.aws.efs.efs_csi.enabled | Enable EFS CSI driver for flow modules | | | | false | |
| flowModules.persistence.storageClass | Storage class for flow modules volume | | | | "" | If empty, uses cloud provider default |
| flowModules.persistence.size | PVC size for flow modules volume | | | | "" | Defaults: AWS=1Mi, Azure=100Gi |
| functions.persistence.aws.efs.enabled | Enable AWS EFS for functions storage | | | | true | For AWS cloud provider only |
| functions.persistence.aws.efs.id | EFS filesystem ID for functions | | | | "" | Required when EFS is enabled |
| functions.persistence.aws.efs.efs_csi.enabled | Enable EFS CSI driver for functions | | | | false | |
| functions.persistence.storageClass | Storage class for functions volume | | | | "" | If empty, uses cloud provider default |
| functions.persistence.size | PVC size for functions volume | | | | "" | Defaults: AWS=1Mi, Azure=100Gi |

## Networking & Ingress Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| tls.enabled | Enable TLS for ingress resources | | | | false | |
| tls.crt | TLS certificate content | | | | "" | Base64-encoded certificate |
| tls.key | TLS private key content | | | | "" | Base64-encoded private key |
| tls.existingSecret | Use existing TLS secret | | | | "" | Secret must contain tls.crt and tls.key |
| ingress.enabled | Enable ingress resources | | | | true | |
| ingress.annotations | Additional ingress annotations | | | | {} | Key-value pairs for ingress resource |
| ingress.hosts | List of ingress hostnames | | | | [] | |
| ingress.tls.enabled | Enable TLS for ingress | | | | false | |
| ingress.tls.secretName | TLS secret name | | | | "" | |
| ingress.forceHttps.enabled | Redirect HTTP to HTTPS | | | | false | |
| managementUi.ingress.enabled | Enable ingress for Management UI | | | | true | |
| managementUi.ingress.host | Hostname for Management UI ingress | | | | "" | |
| managementUi.ingress.tls.enabled | Enable TLS for Management UI ingress | | | | false | |
| managementUi.ingress.tls.existingSecret | TLS secret for Management UI | | | | "" | |
| managementUi.ingress.ipWhiteListMiddleware.enabled | Enable IP whitelisting for Management UI | | | | true | |
| managementUi.ingress.ipWhiteListMiddleware.ipWhiteList.sourceRange | IP ranges allowed to access Management UI | | | | ["0.0.0.0/0"] | Default allows all IPs |

## OAuth & Authentication Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| amazonCredentials.clientId | Amazon Developer client ID | | | | "" | |
| amazonCredentials.clientSecret | Amazon Developer client secret | | | | "" | |
| amazonCredentials.existingSecret | Secret with Amazon credentials | | | | "" | |
| smtpOAuth2.auth.clientId | Email OAuth2 client ID | | | | "" | |
| smtpOAuth2.auth.clientSecret | Email OAuth2 client secret | | | | "" | |
| smtpOAuth2.auth.refreshToken | Email OAuth2 refresh token | | | | "" | |
| smtpOAuth2.auth.accessToken | Email OAuth2 access token | | | | "" | |
| smtpEmailNotificationCredentials.authType | Email notification auth type | | | | "basic" | Options: "basic" or "oauth2" |
| smtpEmailNotificationCredentials.basic.username | Basic auth username | | | | "" | Used when authType="basic" |
| smtpEmailNotificationCredentials.basic.password | Basic auth password | | | | "" | Used when authType="basic" |
| smtpEmailNotificationCredentials.oauth2.user | OAuth2 user email | | | | "" | Used when authType="oauth2" |
| smtpEmailNotificationCredentials.oauth2.clientId | OAuth2 client ID | | | | "" | Used when authType="oauth2" |
| smtpEmailNotificationCredentials.oauth2.clientSecret | OAuth2 client secret | | | | "" | Used when authType="oauth2" |

## HPA Service-specific Configurations

The following HPA configurations apply to specific services when HPA is enabled:

| Service Name | Enabled by Default | Min Replicas | Max Replicas | CPU Target Utilization | Scale Down Window |
|:-------------|:-------------------|:------------|:------------|:------------------------|:------------------|
| serviceAi | true | 3 | 30 | 25% | 900s (15 min) |
| serviceExecution | true | 3 | 30 | 50% | 900s (15 min) |
| serviceResources | true | 3 | 30 | 50% | 900s (15 min) |
| serviceFunctionExecution | true | 3 | 30 | 50% | 900s (15 min) |
| serviceFunctionScheduler | true | 3 | 30 | 50% | 900s (15 min) |
| serviceHandoverInactivity | true | 3 | 30 | 50% | Not specified |
| serviceHttp | true | 3 | 30 | 50% | Not specified |
| serviceInsightsForwarder | false | 2 | 30 | 40% | 900s (15 min) |
| serviceNlpNer | true | 3 | 30 | 50% | Not specified |
| serviceProfiles | true | 3 | 30 | 50% | Not specified |
| serviceRuntimeFileManager | true | 3 | 30 | 50% | Not specified |
| serviceSessionStateManager | true | 3 | 30 | 50% | Not specified |
| serviceNlpOrchestrator | false | 2 | 30 | 60% | 900s (15 min) |
| serviceNlpEmbeddingEn | false | 2 | 30 | 60% | 900s (15 min) |
| serviceNlpEmbeddingGe | false | 2 | 30 | 60% | 900s (15 min) |

## Kubernetes Configuration

| Setting Name | Description | Team Responsible | Hard Limit | Soft Limit | Default Value | Notes |
|:-------------|:-------------|:------------------|:------------|:------------|:--------------|:-------|
| securityContext.runAsUser | User ID to run containers as | | | | 1337 | For RabbitMQ |
| securityContext.runAsGroup | Group ID to run containers as | | | | 1337 | For RabbitMQ |
| extraVolumes | Additional volumes to mount to services | | | | [] | Can be used to mount secrets, configmaps, etc. |
| extraVolumeMounts | Mount points for extra volumes | | | | [] | Used in conjunction with extraVolumes |
| extraEnvVars | Additional environment variables | | | | [] | Can be used to override configuration |
| affinity | Pod affinity/anti-affinity rules | | | | {} | Controls pod placement |
| nodeSelector | Node selection constraints | | | | {} | Controls which nodes pods can be scheduled on |
| tolerations | Pod tolerations for node taints | | | | [] | Controls which nodes pods can be scheduled on |
| priorityClassName | Priority class for pods | | | | "" | Controls pod scheduling priority |

## Internal notes

1. **feature flags** – always test changes in staging before applying them to production. don’t skip this step.  
2. **mongodb settings** – be extra careful when changing connection configs. wrong settings = downtime.  
3. **resource limits** – changes affect performance and stability. monitor closely after updates.  
4. **auth settings** – never commit secrets to git. never print them in logs.  
5. **knowledge search** – this feature is still in dev. do not enable for customers.  
6. **platform llm config** – use correct model and provider when enabling llm features.  
7. **experimental features** – don’t enable `horizontalPodAutoscaler`, `serviceCollaboration`, or `serviceSentinel` in prod unless explicitly told to.  
8. **infra planning** – account for total cpu + memory based on service replicas. check with SRE aggregate usage.  
9. **nlp services** – disabled by default. only enable the language-specific ones you actually need. enabling all = high memory usage.  
10. **high-memory services** – `nlp embedding` + some classifiers need a lot of ram. confirm with SRE node capacity before enabling.  
11. **language support** – for multi-language, turn on the relevant nlp services (e.g. `serviceNlpClassifierScoreDe` for german).  

---

*Note: This documentation is based on the current configuration as of April 2025. Feature flags and settings may change with new releases.*
