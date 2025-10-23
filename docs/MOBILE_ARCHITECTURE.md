# Togo Health - Mobile Architecture

**Version**: 1.0
**Audience**: Technical stakeholders, mobile development teams, investors
**Purpose**: Comprehensive mobile architecture for iOS and Android applications

---

## Executive Summary

Togo Health's mobile applications will deliver the full platform experience optimized for clinicians on-the-go. The mobile architecture prioritizes:

- **Native Performance**: Smooth 60fps UI, fast app startup, efficient battery usage
- **Cross-Platform Efficiency**: Maximum code sharing while maintaining platform-specific excellence
- **Offline-First**: Full functionality without internet connectivity
- **Real-Time Updates**: Instant shift notifications, agent activity, urgent alerts
- **Security**: Biometric authentication, secure storage, certificate pinning
- **Healthcare Compliance**: HIPAA-compliant data handling, audit trails

**Recommended Approach**: **React Native with Expo** (85% code sharing) + Native Modules for critical features

**Alternative**: Native iOS (Swift/SwiftUI) + Native Android (Kotlin/Jetpack Compose) for maximum performance

---

## Mobile Strategy Overview

### Cross-Platform vs Native Decision Matrix

| Factor | React Native + Expo | Native (Swift + Kotlin) |
|--------|---------------------|-------------------------|
| **Development Speed** | ⭐⭐⭐⭐⭐ 85% code reuse | ⭐⭐ Separate codebases |
| **Time to Market** | ⭐⭐⭐⭐⭐ 4-6 months MVP | ⭐⭐⭐ 8-12 months MVP |
| **Performance** | ⭐⭐⭐⭐ Near-native | ⭐⭐⭐⭐⭐ Pure native |
| **Developer Pool** | ⭐⭐⭐⭐⭐ Large (JavaScript) | ⭐⭐⭐ Smaller (native devs) |
| **Maintenance** | ⭐⭐⭐⭐⭐ Single codebase | ⭐⭐ Two codebases |
| **Platform Features** | ⭐⭐⭐⭐ Expo + native modules | ⭐⭐⭐⭐⭐ Full platform access |
| **OTA Updates** | ⭐⭐⭐⭐⭐ Instant via Expo | ⭐⭐ App Store review required |
| **Package Size** | ⭐⭐⭐ ~40-50MB | ⭐⭐⭐⭐ ~15-25MB |
| **Team Synergy** | ⭐⭐⭐⭐⭐ Shares code with web | ⭐⭐ Separate mobile team |

**Recommendation**: **React Native with Expo** for Togo Health due to:
1. Faster development (4-6 months vs 8-12 months to MVP)
2. Code sharing with web frontend (shared business logic, types, utilities)
3. Over-The-Air (OTA) updates for rapid bug fixes and feature rollouts
4. Large talent pool (React developers can contribute)
5. Proven at scale (Microsoft, Shopify, Discord, Coinbase use React Native)

---

## React Native Architecture (Primary Approach)

### Technology Stack

**Core Framework**: React Native 0.73+ with Expo 50+
**Language**: TypeScript 5.3+
**State Management**: Zustand + TanStack Query (React Query)
**Navigation**: React Navigation 6
**UI Components**: React Native Paper + custom design system
**Forms**: React Hook Form + Zod validation
**Real-Time**: Socket.io client
**Local Database**: WatermelonDB (SQLite-based)
**Secure Storage**: expo-secure-store
**Push Notifications**: Expo Notifications + FCM
**Biometrics**: expo-local-authentication
**Camera**: expo-camera (for badge scanning, document upload)
**Background Tasks**: expo-task-manager
**Analytics**: Segment + Sentry
**Testing**: Jest + React Native Testing Library + Detox (E2E)

---

## Project Structure

```
togo-health-mobile/
├── app/                              # Expo Router (file-based routing)
│   ├── (auth)/                       # Authentication flow
│   │   ├── login.tsx
│   │   ├── biometric-setup.tsx
│   │   └── onboarding.tsx
│   ├── (tabs)/                       # Main tab navigation
│   │   ├── dashboard/
│   │   │   ├── index.tsx             # Dashboard home
│   │   │   ├── shift-details.tsx
│   │   │   └── agent-activity.tsx
│   │   ├── shifts/
│   │   │   ├── index.tsx             # Shift list
│   │   │   ├── calendar.tsx
│   │   │   └── swap-request.tsx
│   │   ├── learning/
│   │   │   ├── index.tsx             # Course catalog
│   │   │   ├── course-details.tsx
│   │   │   └── cpd-tracker.tsx
│   │   ├── credentials/
│   │   │   ├── index.tsx             # Credential list
│   │   │   ├── digital-passport.tsx
│   │   │   └── renewal.tsx
│   │   └── profile/
│   │       ├── index.tsx
│   │       ├── settings.tsx
│   │       └── notifications.tsx
│   ├── _layout.tsx                   # Root layout
│   └── +not-found.tsx
│
├── src/
│   ├── components/                   # Reusable UI components
│   │   ├── ui/                       # Base components
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Badge.tsx
│   │   │   └── Avatar.tsx
│   │   ├── agent/                    # Agent-specific components
│   │   │   ├── AgentActivityCard.tsx
│   │   │   ├── AgentApprovalModal.tsx
│   │   │   └── AgentStatusBadge.tsx
│   │   ├── shift/
│   │   │   ├── ShiftCard.tsx
│   │   │   ├── ShiftCalendar.tsx
│   │   │   └── SwapRequestCard.tsx
│   │   └── common/
│   │       ├── Header.tsx
│   │       ├── LoadingSpinner.tsx
│   │       └── ErrorBoundary.tsx
│   │
│   ├── screens/                      # Complex screen compositions
│   │   ├── DashboardScreen/
│   │   ├── ShiftDetailsScreen/
│   │   └── CredentialRenewalScreen/
│   │
│   ├── services/                     # Business logic layer
│   │   ├── api/                      # API clients
│   │   │   ├── graphql/
│   │   │   │   ├── client.ts         # Apollo Client setup
│   │   │   │   ├── queries/
│   │   │   │   ├── mutations/
│   │   │   │   └── fragments/
│   │   │   └── rest/
│   │   │       └── client.ts
│   │   ├── auth/
│   │   │   ├── AuthService.ts        # VO SSO, biometric auth
│   │   │   ├── TokenManager.ts
│   │   │   └── BiometricService.ts
│   │   ├── sync/
│   │   │   ├── SyncEngine.ts         # Offline sync logic
│   │   │   └── ConflictResolver.ts
│   │   ├── notifications/
│   │   │   ├── PushService.ts
│   │   │   └── LocalNotificationService.ts
│   │   └── storage/
│   │       ├── SecureStore.ts
│   │       └── DatabaseService.ts
│   │
│   ├── hooks/                        # Custom React hooks
│   │   ├── useAuth.ts
│   │   ├── useShifts.ts
│   │   ├── useAgentActivity.ts
│   │   ├── useOfflineSync.ts
│   │   ├── useBiometrics.ts
│   │   └── usePushNotifications.ts
│   │
│   ├── store/                        # Zustand stores
│   │   ├── authStore.ts
│   │   ├── userStore.ts
│   │   ├── shiftStore.ts
│   │   └── syncStore.ts
│   │
│   ├── database/                     # WatermelonDB models
│   │   ├── models/
│   │   │   ├── Shift.ts
│   │   │   ├── Credential.ts
│   │   │   ├── LearningRecord.ts
│   │   │   └── AgentActivity.ts
│   │   ├── schema.ts
│   │   └── migrations/
│   │
│   ├── navigation/
│   │   ├── types.ts                  # Navigation type definitions
│   │   └── linking.ts                # Deep linking configuration
│   │
│   ├── utils/
│   │   ├── date.ts
│   │   ├── formatting.ts
│   │   ├── validation.ts
│   │   └── helpers.ts
│   │
│   ├── constants/
│   │   ├── colors.ts
│   │   ├── typography.ts
│   │   └── config.ts
│   │
│   └── types/
│       ├── api.ts
│       ├── models.ts
│       └── navigation.ts
│
├── assets/
│   ├── images/
│   ├── icons/
│   └── fonts/
│
├── app.json                          # Expo configuration
├── eas.json                          # EAS Build configuration
├── babel.config.js
├── tsconfig.json
└── package.json
```

---

## Key Architecture Patterns

### 1. Offline-First Architecture

**Approach**: Local SQLite database (WatermelonDB) as source of truth, sync with server

```typescript
// WatermelonDB model example
import { Model } from '@nozbe/watermelondb';
import { field, date, readonly } from '@nozbe/watermelondb/decorators';

class Shift extends Model {
  static table = 'shifts';

  @field('shift_id') shiftId!: string;
  @field('location') location!: string;
  @field('role') role!: string;
  @date('start_time') startTime!: Date;
  @date('end_time') endTime!: Date;
  @field('status') status!: string;
  @field('synced') synced!: boolean;
  @readonly @date('created_at') createdAt!: Date;
  @readonly @date('updated_at') updatedAt!: Date;
}

// Offline sync service
class OfflineSyncService {
  private database: Database;
  private apiClient: ApiClient;

  async syncShifts() {
    const unsyncedShifts = await this.database
      .get<Shift>('shifts')
      .query(Q.where('synced', false))
      .fetch();

    for (const shift of unsyncedShifts) {
      try {
        // Upload to server
        await this.apiClient.updateShift(shift.shiftId, {
          status: shift.status,
          // ... other fields
        });

        // Mark as synced
        await this.database.write(async () => {
          await shift.update(s => {
            s.synced = true;
          });
        });
      } catch (error) {
        console.error('Failed to sync shift', shift.shiftId, error);
      }
    }
  }

  async downloadNewShifts() {
    const lastSync = await SecureStore.getItemAsync('last_sync_time');
    const newShifts = await this.apiClient.getShifts({
      since: lastSync,
    });

    await this.database.write(async () => {
      for (const shiftData of newShifts) {
        await this.database.get<Shift>('shifts').create(shift => {
          shift.shiftId = shiftData.id;
          shift.location = shiftData.location;
          shift.role = shiftData.role;
          shift.startTime = new Date(shiftData.startTime);
          shift.endTime = new Date(shiftData.endTime);
          shift.status = shiftData.status;
          shift.synced = true;
        });
      }
    });

    await SecureStore.setItemAsync('last_sync_time', new Date().toISOString());
  }
}
```

### 2. Authentication with Verified Orchestration

**Biometric + SSO Flow**:

```typescript
// Authentication service with VO integration
import * as LocalAuthentication from 'expo-local-authentication';
import * as SecureStore from 'expo-secure-store';
import * as WebBrowser from 'expo-web-browser';
import * as AuthSession from 'expo-auth-session';

class AuthService {
  private voConfig = {
    clientId: process.env.EXPO_PUBLIC_VO_CLIENT_ID,
    redirectUri: AuthSession.makeRedirectUri({ scheme: 'togohealth' }),
    scopes: ['openid', 'profile', 'email', 'credentials'],
    discoveryUrl: 'https://auth.verified-orchestration.com/.well-known/openid-configuration',
  };

  // SSO login via Verified Orchestration
  async loginWithVO() {
    const discovery = await AuthSession.fetchDiscoveryAsync(this.voConfig.discoveryUrl);

    const authRequest = new AuthSession.AuthRequest({
      clientId: this.voConfig.clientId,
      redirectUri: this.voConfig.redirectUri,
      scopes: this.voConfig.scopes,
      responseType: AuthSession.ResponseType.Code,
      usePKCE: true,
    });

    const result = await authRequest.promptAsync(discovery);

    if (result.type === 'success') {
      const { code } = result.params;

      // Exchange code for tokens
      const tokenResponse = await AuthSession.exchangeCodeAsync(
        {
          clientId: this.voConfig.clientId,
          code,
          redirectUri: this.voConfig.redirectUri,
          extraParams: {
            code_verifier: authRequest.codeVerifier!,
          },
        },
        discovery
      );

      // Store tokens securely
      await SecureStore.setItemAsync('access_token', tokenResponse.accessToken);
      await SecureStore.setItemAsync('refresh_token', tokenResponse.refreshToken!);
      await SecureStore.setItemAsync('id_token', tokenResponse.idToken!);

      // Fetch user profile
      const userProfile = await this.fetchUserProfile(tokenResponse.accessToken);

      return userProfile;
    } else {
      throw new Error('Authentication failed');
    }
  }

  // Enable biometric authentication (after initial login)
  async enableBiometricAuth() {
    const hasHardware = await LocalAuthentication.hasHardwareAsync();
    const isEnrolled = await LocalAuthentication.isEnrolledAsync();

    if (!hasHardware || !isEnrolled) {
      throw new Error('Biometric authentication not available');
    }

    const supportedTypes = await LocalAuthentication.supportedAuthenticationTypesAsync();
    // supportedTypes: [1 = fingerprint, 2 = facial recognition, 3 = iris]

    // Store biometric preference
    await SecureStore.setItemAsync('biometric_enabled', 'true');
  }

  // Authenticate with biometrics (for subsequent logins)
  async authenticateWithBiometrics() {
    const result = await LocalAuthentication.authenticateAsync({
      promptMessage: 'Authenticate to access Togo Health',
      fallbackLabel: 'Use Passcode',
      cancelLabel: 'Cancel',
      disableDeviceFallback: false,
    });

    if (!result.success) {
      throw new Error('Biometric authentication failed');
    }

    // Retrieve stored tokens
    const accessToken = await SecureStore.getItemAsync('access_token');
    const refreshToken = await SecureStore.getItemAsync('refresh_token');

    if (!accessToken || !refreshToken) {
      throw new Error('No stored credentials');
    }

    // Check if access token is expired
    if (this.isTokenExpired(accessToken)) {
      // Refresh token
      const newTokens = await this.refreshAccessToken(refreshToken);
      await SecureStore.setItemAsync('access_token', newTokens.accessToken);
      return newTokens.accessToken;
    }

    return accessToken;
  }

  // Refresh access token
  private async refreshAccessToken(refreshToken: string) {
    const discovery = await AuthSession.fetchDiscoveryAsync(this.voConfig.discoveryUrl);

    const tokenResponse = await AuthSession.refreshAsync(
      {
        clientId: this.voConfig.clientId,
        refreshToken,
      },
      discovery
    );

    return tokenResponse;
  }

  private isTokenExpired(token: string): boolean {
    const payload = JSON.parse(atob(token.split('.')[1]));
    return payload.exp * 1000 < Date.now();
  }

  private async fetchUserProfile(accessToken: string) {
    const response = await fetch('https://api.verified-orchestration.com/userinfo', {
      headers: {
        Authorization: `Bearer ${accessToken}`,
      },
    });

    return response.json();
  }
}
```

### 3. Real-Time Updates with Socket.io

**WebSocket connection for live agent activity and shift updates**:

```typescript
// Real-time service
import io, { Socket } from 'socket.io-client';

class RealtimeService {
  private socket: Socket | null = null;
  private reconnectAttempts = 0;
  private maxReconnectAttempts = 5;

  async connect(accessToken: string) {
    this.socket = io('wss://api.togohealth.com', {
      auth: {
        token: accessToken,
      },
      transports: ['websocket'],
      reconnection: true,
      reconnectionDelay: 1000,
      reconnectionDelayMax: 5000,
      reconnectionAttempts: this.maxReconnectAttempts,
    });

    this.socket.on('connect', () => {
      console.log('Connected to real-time server');
      this.reconnectAttempts = 0;
    });

    this.socket.on('disconnect', (reason) => {
      console.log('Disconnected:', reason);
    });

    this.socket.on('reconnect_attempt', () => {
      this.reconnectAttempts++;
      console.log(`Reconnect attempt ${this.reconnectAttempts}`);
    });

    // Listen for agent activity updates
    this.socket.on('agent:activity', (data) => {
      this.handleAgentActivity(data);
    });

    // Listen for shift updates
    this.socket.on('shift:updated', (data) => {
      this.handleShiftUpdate(data);
    });

    // Listen for urgent notifications
    this.socket.on('notification:urgent', (data) => {
      this.handleUrgentNotification(data);
    });
  }

  private handleAgentActivity(data: AgentActivityEvent) {
    // Update local database
    database.write(async () => {
      await database.get('agent_activities').create(activity => {
        activity.agentType = data.agentType;
        activity.status = data.status;
        activity.message = data.message;
        activity.timestamp = new Date(data.timestamp);
      });
    });

    // Show push notification if app is in background
    if (AppState.currentState !== 'active') {
      Notifications.scheduleNotificationAsync({
        content: {
          title: `${data.agentType} Update`,
          body: data.message,
          data: { type: 'agent_activity', activityId: data.id },
        },
        trigger: null, // Immediate
      });
    }
  }

  private handleShiftUpdate(data: ShiftUpdateEvent) {
    // Update local shift in WatermelonDB
    database.write(async () => {
      const shift = await database.get<Shift>('shifts').find(data.shiftId);
      await shift.update(s => {
        s.status = data.status;
        s.location = data.location;
        s.synced = true;
      });
    });

    // Notify user
    if (data.status === 'cancelled' || data.status === 'modified') {
      Notifications.scheduleNotificationAsync({
        content: {
          title: 'Shift Update',
          body: `Your shift on ${formatDate(data.startTime)} has been ${data.status}`,
          data: { type: 'shift_update', shiftId: data.shiftId },
        },
        trigger: null,
      });
    }
  }

  private handleUrgentNotification(data: UrgentNotificationEvent) {
    // Critical notifications (e.g., emergency shift coverage needed)
    Notifications.scheduleNotificationAsync({
      content: {
        title: data.title,
        body: data.message,
        priority: Notifications.AndroidNotificationPriority.MAX,
        sound: true,
        vibrate: [0, 250, 250, 250],
        data: { type: 'urgent', ...data.metadata },
      },
      trigger: null,
    });

    // Show in-app alert if user is active
    if (AppState.currentState === 'active') {
      Alert.alert(
        data.title,
        data.message,
        [
          { text: 'Dismiss', style: 'cancel' },
          { text: 'View Details', onPress: () => navigateToDetails(data) },
        ]
      );
    }
  }

  disconnect() {
    this.socket?.disconnect();
    this.socket = null;
  }
}
```

### 4. Push Notifications

**Firebase Cloud Messaging (FCM) + Expo Notifications**:

```typescript
// Push notification service
import * as Notifications from 'expo-notifications';
import * as Device from 'expo-device';
import Constants from 'expo-constants';

// Configure notification handler
Notifications.setNotificationHandler({
  handleNotification: async () => ({
    shouldShowAlert: true,
    shouldPlaySound: true,
    shouldSetBadge: true,
  }),
});

class PushNotificationService {
  async registerForPushNotifications() {
    if (!Device.isDevice) {
      console.warn('Push notifications only work on physical devices');
      return null;
    }

    // Request permissions
    const { status: existingStatus } = await Notifications.getPermissionsAsync();
    let finalStatus = existingStatus;

    if (existingStatus !== 'granted') {
      const { status } = await Notifications.requestPermissionsAsync();
      finalStatus = status;
    }

    if (finalStatus !== 'granted') {
      console.warn('Push notification permission denied');
      return null;
    }

    // Get Expo Push Token
    const expoPushToken = await Notifications.getExpoPushTokenAsync({
      projectId: Constants.expoConfig?.extra?.eas?.projectId,
    });

    // Register token with backend
    await this.registerTokenWithBackend(expoPushToken.data);

    // Configure Android notification channel
    if (Platform.OS === 'android') {
      await Notifications.setNotificationChannelAsync('default', {
        name: 'Default',
        importance: Notifications.AndroidImportance.MAX,
        vibrationPattern: [0, 250, 250, 250],
        lightColor: '#667EEA',
      });

      // Create channels for different notification types
      await Notifications.setNotificationChannelAsync('shift-updates', {
        name: 'Shift Updates',
        importance: Notifications.AndroidImportance.HIGH,
        sound: 'shift_update.wav',
      });

      await Notifications.setNotificationChannelAsync('agent-activity', {
        name: 'Agent Activity',
        importance: Notifications.AndroidImportance.DEFAULT,
      });

      await Notifications.setNotificationChannelAsync('urgent', {
        name: 'Urgent Alerts',
        importance: Notifications.AndroidImportance.MAX,
        vibrationPattern: [0, 500, 250, 500],
        sound: 'urgent_alert.wav',
      });
    }

    return expoPushToken.data;
  }

  async registerTokenWithBackend(token: string) {
    const accessToken = await SecureStore.getItemAsync('access_token');

    await fetch('https://api.togohealth.com/api/v1/push-tokens', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${accessToken}`,
      },
      body: JSON.stringify({
        token,
        platform: Platform.OS,
        deviceId: Constants.deviceId,
      }),
    });
  }

  // Handle notification tap
  setupNotificationListeners(navigation: NavigationProp<any>) {
    // Notification received while app is in foreground
    const notificationListener = Notifications.addNotificationReceivedListener(notification => {
      console.log('Notification received:', notification);
    });

    // Notification tapped by user
    const responseListener = Notifications.addNotificationResponseReceivedListener(response => {
      const data = response.notification.request.content.data;

      // Navigate based on notification type
      switch (data.type) {
        case 'shift_update':
          navigation.navigate('ShiftDetails', { shiftId: data.shiftId });
          break;
        case 'agent_activity':
          navigation.navigate('AgentActivity', { activityId: data.activityId });
          break;
        case 'credential_expiring':
          navigation.navigate('CredentialRenewal', { credentialId: data.credentialId });
          break;
        case 'urgent':
          navigation.navigate('UrgentAlert', { alertId: data.alertId });
          break;
        default:
          navigation.navigate('Dashboard');
      }
    });

    return () => {
      Notifications.removeNotificationSubscription(notificationListener);
      Notifications.removeNotificationSubscription(responseListener);
    };
  }

  // Schedule local notification
  async scheduleLocalNotification(title: string, body: string, data: any, triggerDate?: Date) {
    await Notifications.scheduleNotificationAsync({
      content: {
        title,
        body,
        data,
        sound: true,
        priority: Notifications.AndroidNotificationPriority.HIGH,
      },
      trigger: triggerDate
        ? { date: triggerDate }
        : null, // null = immediate
    });
  }

  // Cancel all scheduled notifications
  async cancelAllNotifications() {
    await Notifications.cancelAllScheduledNotificationsAsync();
  }
}
```

### 5. Background Tasks

**Background sync and shift reminders**:

```typescript
// Background task service
import * as BackgroundFetch from 'expo-background-fetch';
import * as TaskManager from 'expo-task-manager';

const BACKGROUND_SYNC_TASK = 'background-sync-task';
const SHIFT_REMINDER_TASK = 'shift-reminder-task';

TaskManager.defineTask(BACKGROUND_SYNC_TASK, async () => {
  try {
    // Sync data with server
    const syncService = new OfflineSyncService();
    await syncService.syncAll();

    return BackgroundFetch.BackgroundFetchResult.NewData;
  } catch (error) {
    console.error('Background sync failed:', error);
    return BackgroundFetch.BackgroundFetchResult.Failed;
  }
});

TaskManager.defineTask(SHIFT_REMINDER_TASK, async () => {
  try {
    // Check for upcoming shifts
    const database = getDatabase();
    const upcomingShifts = await database
      .get<Shift>('shifts')
      .query(
        Q.where('start_time', Q.between(Date.now(), Date.now() + 4 * 60 * 60 * 1000)), // Next 4 hours
        Q.where('status', 'confirmed')
      )
      .fetch();

    for (const shift of upcomingShifts) {
      const hoursUntilShift = (shift.startTime.getTime() - Date.now()) / (1000 * 60 * 60);

      if (hoursUntilShift <= 2 && hoursUntilShift > 1.9) {
        // Send reminder 2 hours before shift
        await Notifications.scheduleNotificationAsync({
          content: {
            title: 'Shift Reminder',
            body: `Your shift at ${shift.location} starts in 2 hours`,
            data: { type: 'shift_reminder', shiftId: shift.shiftId },
          },
          trigger: null,
        });
      }
    }

    return BackgroundFetch.BackgroundFetchResult.NewData;
  } catch (error) {
    console.error('Shift reminder check failed:', error);
    return BackgroundFetch.BackgroundFetchResult.Failed;
  }
});

class BackgroundTaskService {
  async registerBackgroundSync() {
    await BackgroundFetch.registerTaskAsync(BACKGROUND_SYNC_TASK, {
      minimumInterval: 15 * 60, // 15 minutes
      stopOnTerminate: false,
      startOnBoot: true,
    });
  }

  async registerShiftReminders() {
    await BackgroundFetch.registerTaskAsync(SHIFT_REMINDER_TASK, {
      minimumInterval: 30 * 60, // 30 minutes
      stopOnTerminate: false,
      startOnBoot: true,
    });
  }

  async unregisterAllTasks() {
    await BackgroundFetch.unregisterTaskAsync(BACKGROUND_SYNC_TASK);
    await BackgroundFetch.unregisterTaskAsync(SHIFT_REMINDER_TASK);
  }
}
```

### 6. State Management with Zustand

**Lightweight state management**:

```typescript
// Auth store
import { create } from 'zustand';
import { persist, createJSONStorage } from 'zustand/middleware';
import AsyncStorage from '@react-native-async-storage/async-storage';

interface AuthState {
  isAuthenticated: boolean;
  user: User | null;
  accessToken: string | null;
  biometricEnabled: boolean;
  login: (user: User, accessToken: string) => void;
  logout: () => void;
  enableBiometric: () => void;
}

export const useAuthStore = create<AuthState>()(
  persist(
    (set) => ({
      isAuthenticated: false,
      user: null,
      accessToken: null,
      biometricEnabled: false,

      login: (user, accessToken) => set({
        isAuthenticated: true,
        user,
        accessToken,
      }),

      logout: () => set({
        isAuthenticated: false,
        user: null,
        accessToken: null,
      }),

      enableBiometric: () => set({ biometricEnabled: true }),
    }),
    {
      name: 'auth-storage',
      storage: createJSONStorage(() => AsyncStorage),
      partialize: (state) => ({
        biometricEnabled: state.biometricEnabled,
        // Don't persist sensitive data like tokens
      }),
    }
  )
);

// Sync store (offline sync status)
interface SyncState {
  isSyncing: boolean;
  lastSyncTime: Date | null;
  unsyncedCount: number;
  syncError: string | null;
  startSync: () => void;
  finishSync: (success: boolean, error?: string) => void;
  incrementUnsyncedCount: () => void;
  decrementUnsyncedCount: () => void;
}

export const useSyncStore = create<SyncState>((set) => ({
  isSyncing: false,
  lastSyncTime: null,
  unsyncedCount: 0,
  syncError: null,

  startSync: () => set({ isSyncing: true, syncError: null }),

  finishSync: (success, error) => set({
    isSyncing: false,
    lastSyncTime: success ? new Date() : null,
    syncError: error || null,
  }),

  incrementUnsyncedCount: () => set((state) => ({
    unsyncedCount: state.unsyncedCount + 1,
  })),

  decrementUnsyncedCount: () => set((state) => ({
    unsyncedCount: Math.max(0, state.unsyncedCount - 1),
  })),
}));
```

### 7. Data Fetching with TanStack Query

**Server state caching and synchronization**:

```typescript
// React Query hooks for data fetching
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

// Fetch upcoming shifts
export function useUpcomingShifts() {
  return useQuery({
    queryKey: ['shifts', 'upcoming'],
    queryFn: async () => {
      const response = await apiClient.graphql({
        query: gql`
          query UpcomingShifts {
            me {
              upcomingShifts(limit: 10) {
                id
                location
                role
                startTime
                endTime
                status
              }
            }
          }
        `,
      });

      return response.data.me.upcomingShifts;
    },
    staleTime: 5 * 60 * 1000, // 5 minutes
    gcTime: 10 * 60 * 1000, // 10 minutes
    refetchOnMount: true,
    refetchOnWindowFocus: true,
  });
}

// Fetch agent activity with infinite scroll
export function useAgentActivity() {
  return useInfiniteQuery({
    queryKey: ['agent-activity'],
    queryFn: async ({ pageParam = 0 }) => {
      const response = await apiClient.graphql({
        query: gql`
          query AgentActivity($offset: Int!, $limit: Int!) {
            me {
              agentActivities(offset: $offset, limit: $limit) {
                id
                agentType
                status
                message
                timestamp
                workflowType
              }
            }
          }
        `,
        variables: {
          offset: pageParam,
          limit: 20,
        },
      });

      return response.data.me.agentActivities;
    },
    getNextPageParam: (lastPage, pages) => {
      return lastPage.length === 20 ? pages.length * 20 : undefined;
    },
    staleTime: 30 * 1000, // 30 seconds
  });
}

// Request shift swap
export function useShiftSwap() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: async (swapRequest: ShiftSwapRequest) => {
      const response = await apiClient.graphql({
        query: gql`
          mutation RequestShiftSwap($input: ShiftSwapRequestInput!) {
            requestShiftSwap(input: $input) {
              id
              status
              requestedAt
            }
          }
        `,
        variables: {
          input: swapRequest,
        },
      });

      return response.data.requestShiftSwap;
    },
    onSuccess: () => {
      // Invalidate and refetch shifts
      queryClient.invalidateQueries({ queryKey: ['shifts'] });

      // Show success message
      Alert.alert('Success', 'Shift swap request submitted');
    },
    onError: (error) => {
      Alert.alert('Error', 'Failed to submit shift swap request');
      console.error('Shift swap error:', error);
    },
  });
}

// Approve agent action (Human-in-the-Loop)
export function useApproveAgentAction() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: async ({ agentId, approved }: { agentId: string; approved: boolean }) => {
      const response = await apiClient.graphql({
        query: gql`
          mutation ApproveAgentAction($agentId: ID!, $approved: Boolean!) {
            approveAgentAction(agentId: $agentId, approved: $approved) {
              id
              status
              approvedAt
            }
          }
        `,
        variables: { agentId, approved },
      });

      return response.data.approveAgentAction;
    },
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['agent-activity'] });
    },
  });
}
```

---

## UI Components & Design System

### Custom Component Library

**Based on React Native Paper with custom theming**:

```typescript
// Custom Button component
import { Button as PaperButton } from 'react-native-paper';
import { StyleSheet } from 'react-native';

interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  loading?: boolean;
  disabled?: boolean;
  onPress: () => void;
  children: React.ReactNode;
}

export function Button({
  variant = 'primary',
  size = 'md',
  loading,
  disabled,
  onPress,
  children,
}: ButtonProps) {
  const buttonStyle = [
    styles.base,
    styles[variant],
    styles[size],
    disabled && styles.disabled,
  ];

  return (
    <PaperButton
      mode={variant === 'outline' ? 'outlined' : 'contained'}
      onPress={onPress}
      loading={loading}
      disabled={disabled}
      style={buttonStyle}
      contentStyle={styles.content}
      labelStyle={styles.label}
    >
      {children}
    </PaperButton>
  );
}

const styles = StyleSheet.create({
  base: {
    borderRadius: 10,
  },
  primary: {
    backgroundColor: '#667EEA',
  },
  secondary: {
    backgroundColor: '#6B7280',
  },
  outline: {
    backgroundColor: 'transparent',
    borderColor: '#667EEA',
    borderWidth: 1,
  },
  ghost: {
    backgroundColor: 'transparent',
  },
  sm: {
    height: 36,
  },
  md: {
    height: 44,
  },
  lg: {
    height: 52,
  },
  disabled: {
    opacity: 0.5,
  },
  content: {
    height: '100%',
  },
  label: {
    fontWeight: '600',
  },
});

// Agent Activity Card
interface AgentActivityCardProps {
  activity: AgentActivity;
  onApprove?: () => void;
  onReject?: () => void;
}

export function AgentActivityCard({ activity, onApprove, onReject }: AgentActivityCardProps) {
  const workflowColor = {
    autonomous: '#10B981',
    'human-in-the-loop': '#F59E0B',
    'human-on-the-loop': '#667EEA',
  }[activity.workflowType];

  return (
    <View style={styles.card}>
      <View style={styles.cardHeader}>
        <View style={styles.agentInfo}>
          <Text style={styles.agentIcon}>{getAgentIcon(activity.agentType)}</Text>
          <View>
            <Text style={styles.agentName}>{activity.agentType}</Text>
            <Text style={styles.timestamp}>{formatTimestamp(activity.timestamp)}</Text>
          </View>
        </View>
        <View style={[styles.badge, { backgroundColor: workflowColor }]}>
          <Text style={styles.badgeText}>{activity.status}</Text>
        </View>
      </View>

      <Text style={styles.message}>{activity.message}</Text>

      {activity.workflowType === 'human-in-the-loop' && activity.status === 'pending' && (
        <View style={styles.actions}>
          <Button variant="outline" onPress={onReject}>
            Reject
          </Button>
          <Button variant="primary" onPress={onApprove}>
            Approve
          </Button>
        </View>
      )}
    </View>
  );
}

// Shift Card with swipe actions
import Swipeable from 'react-native-gesture-handler/Swipeable';

interface ShiftCardProps {
  shift: Shift;
  onSwap: () => void;
  onCancel: () => void;
}

export function ShiftCard({ shift, onSwap, onCancel }: ShiftCardProps) {
  const renderRightActions = () => (
    <View style={styles.swipeActions}>
      <TouchableOpacity style={[styles.swipeAction, styles.swapAction]} onPress={onSwap}>
        <Text style={styles.swipeActionText}>Swap</Text>
      </TouchableOpacity>
      <TouchableOpacity style={[styles.swipeAction, styles.cancelAction]} onPress={onCancel}>
        <Text style={styles.swipeActionText}>Cancel</Text>
      </TouchableOpacity>
    </View>
  );

  return (
    <Swipeable renderRightActions={renderRightActions}>
      <View style={styles.shiftCard}>
        <View style={styles.shiftHeader}>
          <Text style={styles.shiftDate}>{formatDate(shift.startTime)}</Text>
          <Badge status={shift.status} />
        </View>
        <Text style={styles.shiftLocation}>{shift.location}</Text>
        <Text style={styles.shiftTime}>
          {formatTime(shift.startTime)} - {formatTime(shift.endTime)}
        </Text>
        <Text style={styles.shiftRole}>{shift.role}</Text>
      </View>
    </Swipeable>
  );
}
```

---

## Performance Optimization

### 1. Image Optimization

```typescript
// Optimized image loading with caching
import { Image } from 'expo-image';

export function OptimizedImage({ uri, ...props }) {
  return (
    <Image
      source={{ uri }}
      placeholder={blurhash} // Low-quality placeholder
      contentFit="cover"
      transition={200}
      cachePolicy="memory-disk"
      {...props}
    />
  );
}
```

### 2. List Performance

```typescript
// FlashList for high-performance lists (better than FlatList)
import { FlashList } from '@shopify/flash-list';

export function ShiftList({ shifts }: { shifts: Shift[] }) {
  return (
    <FlashList
      data={shifts}
      renderItem={({ item }) => <ShiftCard shift={item} />}
      estimatedItemSize={100}
      keyExtractor={(item) => item.id}
      onEndReached={loadMore}
      onEndReachedThreshold={0.5}
    />
  );
}
```

### 3. Code Splitting

```typescript
// Lazy load screens
import { lazy, Suspense } from 'react';

const ShiftDetailsScreen = lazy(() => import('./screens/ShiftDetailsScreen'));

function App() {
  return (
    <Suspense fallback={<LoadingSpinner />}>
      <ShiftDetailsScreen />
    </Suspense>
  );
}
```

---

## Testing Strategy

### Unit Tests with Jest

```typescript
// Component test
import { render, fireEvent } from '@testing-library/react-native';
import { Button } from '../components/ui/Button';

describe('Button', () => {
  it('renders correctly', () => {
    const { getByText } = render(
      <Button onPress={() => {}}>Press Me</Button>
    );

    expect(getByText('Press Me')).toBeTruthy();
  });

  it('calls onPress when pressed', () => {
    const onPress = jest.fn();
    const { getByText } = render(
      <Button onPress={onPress}>Press Me</Button>
    );

    fireEvent.press(getByText('Press Me'));
    expect(onPress).toHaveBeenCalledTimes(1);
  });

  it('is disabled when disabled prop is true', () => {
    const { getByText } = render(
      <Button onPress={() => {}} disabled>
        Press Me
      </Button>
    );

    const button = getByText('Press Me');
    expect(button.props.accessibilityState.disabled).toBe(true);
  });
});
```

### E2E Tests with Detox

```typescript
// E2E test example
describe('Login Flow', () => {
  beforeAll(async () => {
    await device.launchApp();
  });

  it('should login with Verified Orchestration', async () => {
    await element(by.id('login-button')).tap();

    // Wait for WebView to load
    await waitFor(element(by.id('vo-login-webview')))
      .toBeVisible()
      .withTimeout(5000);

    // Fill in credentials
    await element(by.id('email-input')).typeText('test@example.com');
    await element(by.id('password-input')).typeText('password');
    await element(by.id('submit-button')).tap();

    // Should navigate to dashboard
    await waitFor(element(by.id('dashboard-screen')))
      .toBeVisible()
      .withTimeout(10000);
  });

  it('should enable biometric authentication', async () => {
    await element(by.id('profile-tab')).tap();
    await element(by.id('enable-biometric-button')).tap();

    // Mock biometric prompt (in test environment)
    await device.setBiometricEnrollment(true);

    await waitFor(element(by.text('Biometric authentication enabled')))
      .toBeVisible()
      .withTimeout(3000);
  });
});
```

---

## Build & Deployment

### EAS Build Configuration

```json
// eas.json
{
  "cli": {
    "version": ">= 5.9.0"
  },
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal",
      "ios": {
        "simulator": true
      }
    },
    "preview": {
      "distribution": "internal",
      "ios": {
        "simulator": false
      },
      "android": {
        "buildType": "apk"
      }
    },
    "production": {
      "ios": {
        "credentialsSource": "remote",
        "autoIncrement": true
      },
      "android": {
        "buildType": "aab",
        "autoIncrement": true
      }
    }
  },
  "submit": {
    "production": {
      "ios": {
        "appleId": "apple@togohealth.com",
        "ascAppId": "123456789",
        "appleTeamId": "TEAM123"
      },
      "android": {
        "serviceAccountKeyPath": "./google-play-key.json",
        "track": "production"
      }
    }
  }
}
```

### Over-The-Air (OTA) Updates

```typescript
// OTA update service
import * as Updates from 'expo-updates';

class OTAUpdateService {
  async checkForUpdates() {
    try {
      const update = await Updates.checkForUpdateAsync();

      if (update.isAvailable) {
        // Download update in background
        await Updates.fetchUpdateAsync();

        // Show update prompt
        Alert.alert(
          'Update Available',
          'A new version is ready. Restart to apply?',
          [
            { text: 'Later', style: 'cancel' },
            {
              text: 'Restart Now',
              onPress: async () => {
                await Updates.reloadAsync();
              },
            },
          ]
        );
      }
    } catch (error) {
      console.error('Failed to check for updates:', error);
    }
  }

  // Automatically check for updates on app foreground
  setupUpdateListener() {
    const subscription = AppState.addEventListener('change', (nextAppState) => {
      if (nextAppState === 'active') {
        this.checkForUpdates();
      }
    });

    return () => subscription.remove();
  }
}
```

---

## Native iOS Architecture (Alternative)

### Swift + SwiftUI Stack

**Technology Stack**:
- **Language**: Swift 5.9+
- **UI Framework**: SwiftUI (iOS 17+)
- **Architecture**: MVVM + Combine
- **Networking**: URLSession + async/await
- **Local Database**: Core Data + CloudKit
- **Dependency Injection**: Swift Package Manager dependencies
- **Authentication**: AuthenticationServices (ASWebAuthenticationSession for VO SSO)
- **Biometrics**: LocalAuthentication framework
- **Push Notifications**: UserNotifications framework + APNs
- **Background Tasks**: BackgroundTasks framework

### Project Structure

```
TogoHealth-iOS/
├── App/
│   ├── TogoHealthApp.swift           # App entry point
│   └── AppDelegate.swift
├── Core/
│   ├── Network/
│   │   ├── APIClient.swift
│   │   ├── GraphQLClient.swift
│   │   └── WebSocketClient.swift
│   ├── Storage/
│   │   ├── CoreDataStack.swift
│   │   ├── KeychainService.swift
│   │   └── UserDefaults+Extensions.swift
│   ├── Auth/
│   │   ├── AuthenticationService.swift
│   │   ├── BiometricService.swift
│   │   └── VerifiedOrchestrationProvider.swift
│   └── Utilities/
│       ├── DateFormatter+Extensions.swift
│       └── Logger.swift
├── Features/
│   ├── Dashboard/
│   │   ├── Views/
│   │   │   ├── DashboardView.swift
│   │   │   └── AgentActivityView.swift
│   │   ├── ViewModels/
│   │   │   └── DashboardViewModel.swift
│   │   └── Models/
│   │       └── DashboardModels.swift
│   ├── Shifts/
│   │   ├── Views/
│   │   │   ├── ShiftListView.swift
│   │   │   ├── ShiftDetailView.swift
│   │   │   └── ShiftCalendarView.swift
│   │   └── ViewModels/
│   │       └── ShiftViewModel.swift
│   ├── Learning/
│   ├── Credentials/
│   └── Profile/
├── UI/
│   ├── Components/
│   │   ├── Button.swift
│   │   ├── Card.swift
│   │   └── TextField.swift
│   ├── Theme/
│   │   ├── Colors.swift
│   │   ├── Typography.swift
│   │   └── Theme.swift
│   └── Modifiers/
│       └── ViewModifiers.swift
└── Resources/
    ├── Assets.xcassets
    └── Localizable.strings
```

### SwiftUI Example

```swift
// MVVM architecture with Combine
import SwiftUI
import Combine

// View Model
class DashboardViewModel: ObservableObject {
    @Published var shifts: [Shift] = []
    @Published var agentActivities: [AgentActivity] = []
    @Published var isLoading = false
    @Published var error: Error?

    private let apiClient: APIClient
    private var cancellables = Set<AnyCancellable>()

    init(apiClient: APIClient = .shared) {
        self.apiClient = apiClient
    }

    func loadDashboard() async {
        isLoading = true

        do {
            async let shiftsResult = apiClient.fetchUpcomingShifts()
            async let activitiesResult = apiClient.fetchAgentActivities()

            let (shifts, activities) = try await (shiftsResult, activitiesResult)

            await MainActor.run {
                self.shifts = shifts
                self.agentActivities = activities
                self.isLoading = false
            }
        } catch {
            await MainActor.run {
                self.error = error
                self.isLoading = false
            }
        }
    }
}

// View
struct DashboardView: View {
    @StateObject private var viewModel = DashboardViewModel()

    var body: some View {
        NavigationStack {
            ScrollView {
                VStack(spacing: 24) {
                    // Upcoming Shifts
                    ShiftsSectionView(shifts: viewModel.shifts)

                    // Agent Activity Feed
                    AgentActivitySectionView(activities: viewModel.agentActivities)
                }
                .padding()
            }
            .navigationTitle("Dashboard")
            .refreshable {
                await viewModel.loadDashboard()
            }
            .task {
                await viewModel.loadDashboard()
            }
            .overlay {
                if viewModel.isLoading {
                    ProgressView()
                }
            }
        }
    }
}

// VO Authentication
import AuthenticationServices

class VerifiedOrchestrationProvider: NSObject, ObservableObject {
    @Published var isAuthenticated = false
    @Published var user: User?

    private var authSession: ASWebAuthenticationSession?

    func login(presentationContext: ASWebAuthenticationPresentationContextProviding) async throws {
        let authURL = buildAuthorizationURL()
        let redirectScheme = "togohealth"

        return try await withCheckedThrowingContinuation { continuation in
            authSession = ASWebAuthenticationSession(
                url: authURL,
                callbackURLScheme: redirectScheme
            ) { callbackURL, error in
                if let error = error {
                    continuation.resume(throwing: error)
                    return
                }

                guard let callbackURL = callbackURL,
                      let code = URLComponents(url: callbackURL, resolvingAgainstBaseURL: false)?
                          .queryItems?
                          .first(where: { $0.name == "code" })?
                          .value
                else {
                    continuation.resume(throwing: AuthError.invalidCallback)
                    return
                }

                Task {
                    do {
                        let tokens = try await self.exchangeCodeForTokens(code)
                        let user = try await self.fetchUserProfile(accessToken: tokens.accessToken)

                        await MainActor.run {
                            self.user = user
                            self.isAuthenticated = true
                        }

                        continuation.resume()
                    } catch {
                        continuation.resume(throwing: error)
                    }
                }
            }

            authSession?.presentationContextProvider = presentationContext
            authSession?.prefersEphemeralWebBrowserSession = true
            authSession?.start()
        }
    }
}

// Biometric Authentication
import LocalAuthentication

class BiometricService {
    func authenticateWithBiometrics() async throws -> Bool {
        let context = LAContext()
        var error: NSError?

        guard context.canEvaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, error: &error) else {
            throw BiometricError.notAvailable
        }

        let reason = "Authenticate to access Togo Health"

        return try await context.evaluatePolicy(
            .deviceOwnerAuthenticationWithBiometrics,
            localizedReason: reason
        )
    }

    var biometricType: LABiometryType {
        let context = LAContext()
        _ = context.canEvaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, error: nil)
        return context.biometryType // .faceID, .touchID, or .none
    }
}
```

---

## Native Android Architecture (Alternative)

### Kotlin + Jetpack Compose Stack

**Technology Stack**:
- **Language**: Kotlin 1.9+
- **UI Framework**: Jetpack Compose
- **Architecture**: MVVM + Kotlin Coroutines + Flow
- **Networking**: Retrofit + OkHttp
- **Local Database**: Room + DataStore
- **Dependency Injection**: Hilt (Dagger)
- **Authentication**: Chrome Custom Tabs for VO SSO
- **Biometrics**: BiometricPrompt API
- **Push Notifications**: Firebase Cloud Messaging
- **Background Tasks**: WorkManager

### Project Structure

```
TogoHealth-Android/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/togohealth/
│   │   │   │   ├── TogoHealthApplication.kt
│   │   │   │   ├── data/
│   │   │   │   │   ├── repository/
│   │   │   │   │   ├── local/
│   │   │   │   │   │   ├── dao/
│   │   │   │   │   │   ├── entity/
│   │   │   │   │   │   └── TogoHealthDatabase.kt
│   │   │   │   │   ├── remote/
│   │   │   │   │   │   ├── api/
│   │   │   │   │   │   └── dto/
│   │   │   │   │   └── model/
│   │   │   │   ├── di/
│   │   │   │   │   ├── NetworkModule.kt
│   │   │   │   │   └── DatabaseModule.kt
│   │   │   │   ├── ui/
│   │   │   │   │   ├── dashboard/
│   │   │   │   │   │   ├── DashboardScreen.kt
│   │   │   │   │   │   └── DashboardViewModel.kt
│   │   │   │   │   ├── shifts/
│   │   │   │   │   ├── learning/
│   │   │   │   │   ├── credentials/
│   │   │   │   │   ├── theme/
│   │   │   │   │   │   ├── Color.kt
│   │   │   │   │   │   ├── Theme.kt
│   │   │   │   │   │   └── Type.kt
│   │   │   │   │   └── components/
│   │   │   │   └── util/
│   │   │   └── res/
│   │   └── test/
│   └── build.gradle.kts
└── build.gradle.kts
```

### Jetpack Compose Example

```kotlin
// View Model with Kotlin Flow
@HiltViewModel
class DashboardViewModel @Inject constructor(
    private val shiftRepository: ShiftRepository,
    private val agentRepository: AgentRepository
) : ViewModel() {

    private val _uiState = MutableStateFlow<DashboardUiState>(DashboardUiState.Loading)
    val uiState: StateFlow<DashboardUiState> = _uiState.asStateFlow()

    init {
        loadDashboard()
    }

    fun loadDashboard() {
        viewModelScope.launch {
            _uiState.value = DashboardUiState.Loading

            try {
                val shifts = shiftRepository.getUpcomingShifts()
                val activities = agentRepository.getRecentActivities()

                _uiState.value = DashboardUiState.Success(
                    shifts = shifts,
                    agentActivities = activities
                )
            } catch (e: Exception) {
                _uiState.value = DashboardUiState.Error(e.message ?: "Unknown error")
            }
        }
    }
}

sealed interface DashboardUiState {
    object Loading : DashboardUiState
    data class Success(
        val shifts: List<Shift>,
        val agentActivities: List<AgentActivity>
    ) : DashboardUiState
    data class Error(val message: String) : DashboardUiState
}

// Composable Screen
@Composable
fun DashboardScreen(
    viewModel: DashboardViewModel = hiltViewModel()
) {
    val uiState by viewModel.uiState.collectAsState()

    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Dashboard") },
                colors = TopAppBarDefaults.topAppBarColors(
                    containerColor = MaterialTheme.colorScheme.primary
                )
            )
        }
    ) { paddingValues ->
        when (val state = uiState) {
            is DashboardUiState.Loading -> {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    CircularProgressIndicator()
                }
            }

            is DashboardUiState.Success -> {
                LazyColumn(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(paddingValues),
                    contentPadding = PaddingValues(16.dp),
                    verticalArrangement = Arrangement.spacedBy(24.dp)
                ) {
                    item {
                        ShiftsSection(shifts = state.shifts)
                    }

                    item {
                        AgentActivitySection(activities = state.agentActivities)
                    }
                }
            }

            is DashboardUiState.Error -> {
                ErrorView(
                    message = state.message,
                    onRetry = { viewModel.loadDashboard() }
                )
            }
        }
    }
}

// Custom Card Component
@Composable
fun ShiftCard(
    shift: Shift,
    onClick: () -> Unit,
    modifier: Modifier = Modifier
) {
    Card(
        onClick = onClick,
        modifier = modifier.fillMaxWidth(),
        elevation = CardDefaults.cardElevation(defaultElevation = 2.dp)
    ) {
        Column(
            modifier = Modifier.padding(16.dp),
            verticalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            Row(
                modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text(
                    text = shift.formattedDate,
                    style = MaterialTheme.typography.titleMedium,
                    fontWeight = FontWeight.Bold
                )
                StatusBadge(status = shift.status)
            }

            Text(
                text = shift.location,
                style = MaterialTheme.typography.bodyLarge
            )

            Text(
                text = "${shift.formattedStartTime} - ${shift.formattedEndTime}",
                style = MaterialTheme.typography.bodyMedium,
                color = MaterialTheme.colorScheme.onSurfaceVariant
            )

            Text(
                text = shift.role,
                style = MaterialTheme.typography.bodySmall,
                color = MaterialTheme.colorScheme.primary
            )
        }
    }
}

// Biometric Authentication
class BiometricAuthenticator(private val context: Context) {

    suspend fun authenticate(): Result<Boolean> = suspendCancellableCoroutine { continuation ->
        val executor = ContextCompat.getMainExecutor(context)
        val biometricPrompt = BiometricPrompt(
            context as FragmentActivity,
            executor,
            object : BiometricPrompt.AuthenticationCallback() {
                override fun onAuthenticationSucceeded(result: BiometricPrompt.AuthenticationResult) {
                    continuation.resume(Result.success(true))
                }

                override fun onAuthenticationError(errorCode: Int, errString: CharSequence) {
                    continuation.resume(Result.failure(BiometricAuthException(errString.toString())))
                }

                override fun onAuthenticationFailed() {
                    continuation.resume(Result.failure(BiometricAuthException("Authentication failed")))
                }
            }
        )

        val promptInfo = BiometricPrompt.PromptInfo.Builder()
            .setTitle("Authenticate to Togo Health")
            .setSubtitle("Use your fingerprint or face")
            .setNegativeButtonText("Cancel")
            .build()

        biometricPrompt.authenticate(promptInfo)
    }
}
```

---

## Mobile Technology Stack Comparison

| Feature | React Native + Expo | Native iOS (Swift) | Native Android (Kotlin) |
|---------|---------------------|-------------------|------------------------|
| **Development Time** | 4-6 months | 6-8 months | 6-8 months |
| **Code Reuse** | 85% shared | 0% | 0% |
| **Performance** | 90-95% native | 100% native | 100% native |
| **OTA Updates** | Yes (instant) | No (App Store) | No (Play Store) |
| **Team Size** | 2-3 developers | 2-3 iOS developers | 2-3 Android developers |
| **Maintenance** | Single codebase | Separate iOS codebase | Separate Android codebase |
| **App Size** | 40-50 MB | 20-30 MB | 15-25 MB |
| **Startup Time** | 1.5-2.5s | 0.8-1.5s | 0.8-1.5s |
| **Battery Usage** | Good | Excellent | Excellent |
| **Platform Features** | Most available | All available | All available |

---

## Recommendation: React Native + Expo

**For Togo Health, React Native with Expo is the recommended approach** because:

1. **Faster Time to Market**: 4-6 months vs 8-12 months for native
2. **Cost Efficiency**: Single team maintains both platforms
3. **Code Sharing**: Shared business logic, types, utilities with web frontend
4. **OTA Updates**: Critical bug fixes deployed instantly without app store approval
5. **Developer Talent**: Larger pool of React developers than native specialists
6. **Proven at Scale**: Used by Microsoft Teams, Shopify, Discord, Coinbase
7. **Native Performance**: With proper optimization, achieves 90-95% native performance
8. **Healthcare Compliance**: HIPAA-compliant with proper implementation (encryption, secure storage, audit trails)

**When to Consider Native**:
- App requires maximum performance (not typical for Togo Health use case)
- Heavy use of platform-specific APIs (Togo Health features work well with Expo)
- Unlimited budget and timeline
- Separate mobile development team already exists

---

## Mobile-Specific Features

### Deep Linking

```typescript
// Deep link configuration
const linking: LinkingOptions<RootStackParamList> = {
  prefixes: ['togohealth://', 'https://app.togohealth.com'],
  config: {
    screens: {
      Dashboard: 'dashboard',
      ShiftDetails: 'shifts/:shiftId',
      AgentActivity: 'agents/:activityId',
      CredentialRenewal: 'credentials/:credentialId/renew',
      LearningCourse: 'learning/courses/:courseId',
      Profile: 'profile',
    },
  },
};

// Handle deep links from push notifications
Notifications.addNotificationResponseReceivedListener(response => {
  const data = response.notification.request.content.data;

  if (data.deepLink) {
    Linking.openURL(data.deepLink);
  }
});

// Handle universal links from web
Linking.addEventListener('url', ({ url }) => {
  const { path, queryParams } = Linking.parse(url);

  // Navigate based on path
  navigation.navigate(path, queryParams);
});
```

### Camera Integration

```typescript
// Document scanning with expo-camera
import { Camera, CameraType } from 'expo-camera';

function DocumentScannerScreen() {
  const [permission, requestPermission] = Camera.useCameraPermissions();
  const [scannedImage, setScannedImage] = useState<string | null>(null);

  const takePicture = async () => {
    if (cameraRef.current) {
      const photo = await cameraRef.current.takePictureAsync({
        quality: 0.8,
        base64: true,
      });

      // Upload document to backend
      await uploadDocument(photo.uri);
    }
  };

  if (!permission?.granted) {
    return (
      <View>
        <Text>Camera permission required</Text>
        <Button onPress={requestPermission}>Grant Permission</Button>
      </View>
    );
  }

  return (
    <Camera
      ref={cameraRef}
      style={styles.camera}
      type={CameraType.back}
    >
      <View style={styles.controls}>
        <Button onPress={takePicture}>Scan Document</Button>
      </View>
    </Camera>
  );
}
```

### Haptic Feedback

```typescript
// Haptic feedback for user actions
import * as Haptics from 'expo-haptics';

// Light feedback for button taps
const handleButtonPress = () => {
  Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Light);
  // ... button action
};

// Medium feedback for important actions
const handleApprove = () => {
  Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Medium);
  // ... approve action
};

// Heavy feedback for critical actions
const handleCancelShift = () => {
  Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Heavy);
  // ... cancel action
};

// Success notification
const handleSuccess = () => {
  Haptics.notificationAsync(Haptics.NotificationFeedbackType.Success);
};

// Error notification
const handleError = () => {
  Haptics.notificationAsync(Haptics.NotificationFeedbackType.Error);
};
```

---

## Mobile Deployment Timeline

### Phase 1: Foundation (Months 1-2)
- Set up React Native + Expo project
- Implement authentication (VO SSO + biometric)
- Build core UI components and design system
- Implement offline database (WatermelonDB)
- Set up push notifications

### Phase 2: Core Features (Months 3-4)
- Dashboard screen with upcoming shifts
- Agent activity feed with real-time updates
- Shift list and calendar views
- Credential management screens
- Profile and settings

### Phase 3: Advanced Features (Months 5-6)
- Shift swap functionality
- Learning course browser
- Digital Passport integration
- Document scanning (camera)
- Background sync and reminders

### Phase 4: Testing & Launch (Months 7-8)
- Performance optimization
- E2E testing with Detox
- Beta testing with pilot users
- App Store and Play Store submission
- Production launch

---

## Conclusion

The recommended mobile architecture for Togo Health uses **React Native with Expo**, providing:

- **85% code sharing** between iOS and Android
- **Faster development** (4-6 months to MVP)
- **OTA updates** for instant bug fixes
- **Native performance** with proper optimization
- **Healthcare compliance** (HIPAA, biometric auth, secure storage)
- **Integration with Verified Orchestration** for SSO and credential verification
- **Offline-first** architecture for reliable operation in low-connectivity environments
- **Real-time updates** via WebSocket for agent activity and shift changes
- **Professional UI** with React Native Paper and custom components

This architecture positions Togo Health's mobile app as a **best-in-class clinician experience** while maintaining development efficiency and code quality across platforms.
