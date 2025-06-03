# Shopping List App Development Guide

This guide outlines the steps for building a synchronized shopping list application across Android, iOS, and Web.

## Step 1: Project Setup

1. **Install dependencies**
   ```bash
   npm install -g expo-cli
   ```
2. **Initialize React Native (Expo) project**
   ```bash
   expo init shoppinglist-mobile
   # Choose blank (TypeScript) template
   ```
3. **Initialize React.js project for web**
   ```bash
   npx create-react-app shoppinglist-web --template typescript
   ```
4. **Add Firebase to both projects**
   ```bash
   cd shoppinglist-mobile
   expo install firebase
   cd ../shoppinglist-web
   npm install firebase
   ```

## Step 2: User Authentication

1. **Enable Firebase Authentication** in the Firebase console for Email/Password and Google providers.
2. **React Native Example**
   - Use `TextInput` components for email and password.
   - Validate input and call `firebase.auth().createUserWithEmailAndPassword` or `signInWithEmailAndPassword`.
3. **React.js Example**
   - Use a form with controlled components.
   - Implement validation and call the same Firebase auth methods.

## Step 3: Database Setup and Real-Time Sync

1. **Firestore Schema**
   - `lists` collection
     - `name: string`
     - `owner: userId`
     - `sharedWith: userId[]`
   - `lists/{listId}/items` subcollection
     - `text: string`
     - `checked: boolean`
2. **Connect to Firestore** using `onSnapshot` for real-time updates in both apps.

## Step 4: Core App Functionality

1. **Create a list** using `addDoc` in Firestore.
2. **Add/Remove/Update items** via Firestore `setDoc`, `updateDoc`, and `deleteDoc`.
3. **Share lists** by updating the `sharedWith` array.
4. **Listen to changes** with real-time listeners so all devices stay in sync.

## Step 5: User Interface and UX

1. **Mobile**: Use React Native components and styling to display lists and items.
2. **Web**: Use Tailwind CSS for responsive design.
3. **Invite Users**: Input field for email addresses to add to `sharedWith`.

## Step 6: Error Handling & Notifications

- Catch and display authentication and Firestore errors.
- Optionally use Toast notifications or modals to inform users of success/failure states.

## Step 7: Deployment

1. **Expo**: Build Android and iOS binaries using `eas build`.
2. **Web**: Deploy to Firebase Hosting or other services like Vercel.

## Step 8: Testing & Debugging

- Use Jest with React Native Testing Library and React Testing Library to create unit tests.
- Debug by checking Firebase logs and using Expo's debugging tools.

