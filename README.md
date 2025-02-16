# Expo Camera and AsyncStorage Race Condition

This repository demonstrates a bug and its solution related to a race condition between Expo's Camera component and AsyncStorage. The issue occurs when storing image URIs captured by the Camera into AsyncStorage.  The problem stems from a potential race condition where the temporary URI provided by the Camera might get deleted before AsyncStorage finishes storing it, leading to app crashes or unexpected behavior.

## Bug

The `bug.js` file showcases the problematic code. It uses the Expo Camera to capture an image and immediately attempts to save its URI to AsyncStorage.  Under certain circumstances (like heavy app load or low memory), the temporary URI becomes invalid before AsyncStorage completes the write operation, resulting in an error.

## Solution

The `bugSolution.js` file provides a robust solution. It addresses the race condition by ensuring the URI persists until AsyncStorage successfully completes the save operation. The key change involves using a mechanism (e.g. Promise and await) to confirm the image URI is stored before moving on. This prevents the temporary file from being prematurely deleted.

## How to reproduce

1. Clone this repository.
2. Install dependencies: `npm install` or `yarn install`.
3. Run the app: `expo start`.
4. Take a picture with the Camera. Observe the app's behavior and examine the console for any errors (bug.js).
5. Repeat step 4 but now run the solution code (bugSolution.js) from the solution branch. Note the improved stability and lack of errors.