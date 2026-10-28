# Mansparsha Book Website

A static, mobile-friendly companion page for the Heyzine flipbook with Firebase Anonymous Authentication, shared likes, and moderated reader reviews.

## Already configured
- Heyzine URL: https://heyzine.com/flip-book/4e7d9baeba.html
- Firebase project: mansparsha-book
- Firebase web config is in `index.html`
- Book ID: `mansparsha`

## Before publishing
1. In Firebase Console > Authentication > Sign-in method, enable **Anonymous**.
2. In Firestore Database > Rules, publish the contents of `firestore.rules`.
3. In Firebase Console > Project settings > General > Your apps, open the web app settings and add your deployed website's domain under Authentication > Settings > Authorized domains if it is not already allowed.
4. Deploy the folder using Firebase Hosting (steps below).

## Deploy with Firebase Hosting

These commands require a computer with Node.js installed. If you only have a phone, use a trusted computer or a cloud development environment that supports terminal commands.

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
```

When asked:
- Use existing project: `mansparsha-book`
- Public directory: `.`
- Configure as a single-page app: `No`
- Set up automatic builds: `No`

Then deploy:

```bash
firebase deploy --only hosting
```

The CLI may ask about overwriting `firebase.json`; choose to keep the supplied configuration or merge it carefully. Hosting should provide a `web.app` URL.

## Approving reviews
1. Open Firebase Console > Firestore Database > Data.
2. Browse to `books` > `mansparsha` > `reviews`.
3. Open a review document.
4. Change its `approved` field from `false` to `true` in the Firebase Console.
5. Save. It will then appear in the public review list.

Only approve appropriate reviews. Never change the database rules to allow everyone to approve reviews.

## Important notes
- Firebase config values used by a browser app are not service-account secrets. Database security rules are what protect data.
- Likes are one per anonymous Firebase user ID. Clearing browser data or using another browser/device can create another anonymous ID, so this is not strong anti-abuse protection.
- This starter page does not include an admin panel. Review approval is done in the Firebase Console.
- Free-plan quotas apply. No provider can guarantee a site will run forever, and Firebase may change free-plan terms.
- The review query uses `approved == true` and `createdAt` ordering. If Firestore asks for a composite index, follow the generated index link in the browser console.
