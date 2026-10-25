# UCEOU Mechanical Engineering Attendance Website

A mobile-friendly personal attendance tracker shared as one website for your class. Each student signs in with their own verified email account. Firestore rules restrict each student to their own attendance records.

## Important limits
- This is a student-maintained tracker, not an official UCEOU attendance system.
- There is no teacher/admin account and no shared class register in this version.
- Percentages are calculated from sessions that the student records. For accurate percentages, record every class, including absences.
- A 3-hour lab/workshop/drawing is recorded as all Present (3 hours) or all Absent (0 present hours, 3 scheduled hours).
- The subject list can be edited in `index.html` if your official subject names differ.

## Part A — Create Firebase project (Safari on iPad)

1. Open https://console.firebase.google.com/ and sign in with Google.
2. Tap **Create a project**. Name it `uceou-mech-attendance`. Follow the prompts.
3. In the project, open **Build → Authentication → Get started**.
4. Open **Sign-in method** and enable **Email/Password**. Save.
5. Open **Build → Firestore Database → Create database**. Choose production mode. Pick a nearby location if offered; database location cannot easily be changed later.
6. Open **Project settings** (gear icon) → **General** → **Your apps** → web icon `</>`.
7. Register an app named `UCEOU Attendance Web`. You do not need to set up Firebase Hosting.
8. Firebase shows a `firebaseConfig` object. Keep that page open or copy its values somewhere private. The web config is not a password, but don't post screenshots of your whole console publicly.

## Part B — Add the Firebase config

1. Open `index.html` in the GitHub editor after you create the repository (Part D below), or edit it in a code editor app.
2. Find the `const firebaseConfig = { ... }` block.
3. Replace each `PASTE_..._HERE` value with the matching value from Firebase. Keep the quotation marks and commas. `projectId` is just the project ID; `authDomain` usually ends with `.firebaseapp.com`.
4. Save/commit the file.

## Part C — Set secure Firestore rules

1. Firebase console → **Firestore Database** → **Rules**.
2. Replace the editor contents with everything in `firestore.rules` from this project.
3. Tap **Publish**.

These rules allow only a signed-in, email-verified user to read/write documents under their own UID. They do not allow students to read other students' records. Do not use public rules such as `allow read, write: if true`.

## Part D — Publish on GitHub Pages

1. Open https://github.com/ in Safari and sign in/create an account.
2. Tap **+** → **New repository**. Name it `uceou-mech-attendance`. Set it to **Public** (GitHub Pages on the free plan typically requires a public repository). Do not upload private student data to this repository.
3. Create/upload `index.html`. On the repo page, use **Add file → Create new file**, name it `index.html`, paste the full contents from this project's `index.html`, and commit.
4. Add a second file named `firestore.rules` and paste the rules file too. This file is documentation; Firebase does not automatically deploy it from GitHub.
5. Repository **Settings → Pages**. Under Build and deployment, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then Save.
6. Wait a minute or two. Refresh Pages settings and open the published URL, usually `https://YOUR-GITHUB-USERNAME.github.io/uceou-mech-attendance/`.
7. If Firebase Authentication has an **Authorized domains** section, open Authentication → Settings → Authorized domains and add `YOUR-GITHUB-USERNAME.github.io`. If it is already listed, no action is needed.

## Part E — Test before sharing

1. Open the published site. Enter your email and a strong unique password, then tap **Create account**.
2. Open your email and tap the verification link.
3. Return to the website and sign in. Record a test class, then reload the page and check it remains.
4. Test with a second email/account. Confirm the second account does not see the first account's records.
5. Only after both tests work, share the website link with your classmates.

## Student instructions

1. Open the same website link.
2. Create an account with an email you can access.
3. Verify the email, then sign in.
4. Select date, subject, session name and duration.
5. Tap **Present** or **Absent**. It saves automatically.
6. Use the same date, subject and session name to correct an existing mark; it updates that record. Delete is available for your own records.

## iPad tips
- In Safari, use the GitHub website's **Add file → Create new file** editor. For long code, landscape orientation can be easier.
- Paste the full `index.html` from a text/code editor app or the downloaded project file. Avoid typing the code manually.
- If the Firebase config is missing, the page will show a setup message and disable sign-in.
- If sign-in works but attendance saving fails, check that Firestore rules were published and the email is verified.
- Keep your Firebase project owner account secure with a strong password and two-factor authentication.

## Current behavior / assumptions
- Subjects included: Mathematics, Communicative English, Engineering Mechanics, Engineering Chemistry, Engineering Drawing, Workshop Practice, Engineering Chemistry Lab, Communicative English Lab.
- Session IDs use date + subject + session name. Use consistent session names (for example, `Period 1`, `Period 2`, `Lab`) so you don't accidentally create duplicates.
- One-hour and two-hour sessions are supported. Three-hour labs/workshop/drawing count as 3 hours if Present and 0 present hours if Absent.
- The app does not automatically import your timetable or attendance from university systems.
