# Exam

## Overview

This exam requires you to enhance a **Car App** by working on both its frontend and backend components. The application includes public **GET** routes and protected **POST**, **PUT**, and **DELETE** routes.

Your primary objective is to improve the app's models and functionality. Key details include:

- **Model Variations:** There are **four versions** of the Car and User models (A, B, C, or D). These models are available [here](./material/models.md).  
- **Your Assignment:** The specific model assigned to **you** can be found [here](./material/Exam.png).

### Exam Structure

The exam consists of **five iterations** (total: 200 points):

- **Iteration 1:**  40 points  
- **Iteration 2:**  40 points  
- **Iteration 3:**  40 points  
- **Iteration 4:**  40 points  
- **Iteration 5:**  40 points  

### Exam Guidelines

To ensure fairness and consistency:

- All work must be committed and pushed to GitHub within **1 hour 15min** of the exam start.
- External monitors are not allowed. Use only your laptop’s built‑in screen.


**Exam Recording Instructions**

- *Recording Requirement*: The coding session must be recorded on your local machine.  
- *Retention Period*: Do not delete the recording until **17th of December**.  
- *Possible Review Situations*: I may request your recording if:  
  - You do not push to GitHub immediately after committing an iteration.  
  - I suspect the use of coding agents.  
  - There is noticeable similarity in code submissions.  
- *How to Record*: Follow the steps outlined in [Recording with Zoom](./material/recording.md). We will review these instructions together before starting the exam.  


**Commit and Push Every Change**

To ensure proper grading:
- At the end of each iteration, make a **commit** with the message format:  
  ```
  [iteration X]: <points> graded
  ```
  where **X** is the iteration number.  
- Immediately run `git push` to upload your changes.  
- Verify that your commits appear in the remote repository.  
- Failure to push commits may result in incomplete grading.

---

### Iteration 1:  **40 points**

1. **Set up** 
   - Clone the [exam starter code](https://github.com/tx00-web-en/exam-starter) repository and name it `exam-project` 
   - Create a **private** GitHub repository, `exam-project`  
   - Add the user `55d41251` as a collaborator to your repository.
   - Initialize a git repository in the `exam-project` project folder:  
     ```sh
     git init
     git add .
     git commit -m "[iteration 1]: Set up repository with initial files"
     ``` 
   - *Push your work to GitHub*

2. **Set Up the Backend**
   - Navigate to the `backend` directory. 
   - Install these dependencies:
      ```sh
      npm install express dotenv cors mongoose jsonwebtoken bcryptjs colors validator cross-env
      ```
   - Install Dev Dependencies
      ```sh
      npm install nodemon jest supertest -D
      ```
   - Run the tests to **ensure** all provided tests **pass**   
   - *Start the backend server*: `npm run dev`

3. **Set Up the Frontend**  
   - Navigate to the `frontend` directory.  
   - Install the necessary dependencies and *start the frontend application*

4. **Fix the User Registration Issue**  

   - The frontend application currently crashes when a new user tries to register with an email that already exists in the database.  
   - Update the relevant code in the frontend, so that duplicate email registrations are handled gracefully.  
   - A complete solution should:  
     - Prevent the crash.  
     - Detect when the email already exists.  
     - Return or display a clear error message (e.g., *Email already in use*).  
   - If you cannot fully fix the issue, implement a partial solution that ensures the application does not crash and communicates the error appropriately.

5. **Self-Assessment and Commit**  
   - Create a **commit** in your Git repository that includes the iteration status and your **self-assessed score** for **this iteration only**, out of **40 points**. 
   - To receive the **maximum points**, your code must **work as intended**, and run **without crashing**.     
   - **Example** *commit message*:  
     ```  
     [iteration 1]: grade 20 out of 40 points
     ```  
   - Push the updated code to your GitHub repository.
   - **Important:** Failure to push commits may result in incomplete grading.

---

## Iteration 2:  **40 points**

1. **Explain Changes to `deleteCar()` Controller: 20 Points**  
   - In the backend, refer to the `deleteCar()` controller. Currently, the car is deleted using the following line: 
     ```js
     const car = await Car.findByIdAndDelete({ _id: id });
     ```
   - This deletes the car based solely on its `id`.    
   - Uncomment the following lines and comment the previous line. Explain how this change affects the functionality and authorization of the app.
     ```js
     const user_id = req.user._id;
     const car = await Car.findByIdAndDelete({ _id: id, user_id: user_id });
     ```
     
   - Add your **explanations as comments in the source code.**
   - Here’s the full `deleteCar()` function for reference:
      ```js
      const deleteCar = async (req, res) => {
        const { id } = req.params;
        try {
          // const user_id = req.user._id;
          // const car = await Car.findByIdAndDelete({ _id: id, user_id: user_id });
          const car = await Car.findByIdAndDelete({ _id: id });
          if (!car) {
            return res.status(404).json({ message: 'car not found' });
          }
          res.status(204).json({ message: 'car deleted successfully' });
        } catch (error) {
          console.error(error);
          res.status(500).json({ error: 'Server Error' });
        }
      };
   ```
      
2. **Explain Changes to `updateCar()` Controller: 20 Points**  
   - In the backend, refer to the `updateCar()` controller. The current update code uses:
     ```js
     { _id: id }
     ```
     This allows any car with the matching `id` to be updated.

   - Uncomment the following block and comment the previous line. Explain how this change affects the functionality and authorization of the app:
     ```js
     const user_id = req.user._id;
     { _id: id, user_id: user_id }
     ```
   - Add your **explanations as comments in the source code**.
   - Here’s the full `updateCar()` function for reference:
      ```js
      const updateCar = async (req, res) => {
        const { id } = req.params;
        try {
          // const user_id = req.user._id;
          const car = await Car.findOneAndUpdate(
            // { _id: id, user_id: user_id },
            { _id: id },
            { ...req.body },
            { new: true }
          );
          if (!car) {
            return res.status(404).json({ message: 'car not found' });
          }
          res.status(200).json(car);
        } catch (error) {
          console.error(error);
          res.status(500).json({ error: 'Server Error' });
        }
      };
      ``` 

3. **Self-Assessment and Commit**  
   - Create a **commit** in your Git repository that includes the iteration status and your **self-assessed score** for **this iteration only**, out of **40 points**. 
   - **Example** *commit message*:  
     ```  
     [iteration 2]: grade 20 out of 40 points
     ```  
   - Push the updated code to your GitHub repository.
   - **Important:** Failure to push commits may result in incomplete grading.

---


### Iteration 3:  **40 points**

1. **Refactor `EditCarPage.jsx`: 15 Points**
   - In `frontend/src/pages/EditCarPage.jsx`, refactor the current state management for form fields to use the `useField` hook from `frontend/src/hooks/useField.jsx`.
   - Ensure that at least one form field (e.g., make, availability, etc.) is updated to use the `useField` hook for state management.
   - Verify that the form works correctly after the refactor.

2. **Self-Assessment and Commit**  
   - Create a **commit** in your Git repository that includes the iteration status and your **self-assessed score** for **this iteration only**, out of **40 points**. 
   - To receive the **maximum points**, your code must **work as intended**, and run **without crashing**.     
   - **Example** *commit message*:  
     ```  
     [iteration 3]: grade 20 out of 40 points
     ```  
   - Push the updated code to your GitHub repository.
   - **Important:** Failure to push commits may result in incomplete grading.

---

### Iteration 4:  **40 points**

1. **Unify `useLogin` and `useSignup` Hooks:**
   - The `useLogin` and `useSignup` custom hooks have significant overlap.
   - Refactor the `useLogin` and `useSignup` custom hooks by creating a single, unified `useAuth` hook.
   - Replace `useLogin` in the `Login` page and `useSignup` in the `Signup` page with this new hook.
   - Ensure both Login and Signup handle their validation rules correctly


2. **Self-Assessment and Commit**  
   - Create a **commit** in your Git repository that includes the iteration status and your **self-assessed score** for **this iteration only**, out of **40 points**. 
   - To receive the **maximum points**, your code must **work as intended**, and run **without crashing**.     
   - **Example** *commit message*:  
     ```  
     [iteration 4]: grade 20 out of 40 points
     ```  
   - Push the updated code to your GitHub repository.
   - **Important:** Failure to push commits may result in incomplete grading.

---

### Iteration 5:  **40 points**

1. Currently, the backend is using port **4000**. Update `.env` to run on port **4001**. 
2. After completing step 1, the frontend will no longer connect to the backend. Make the necessary update in the frontend (`vite.config.js`) so that it connects to the backend.

3. **Self-Assessment and Commit**  
   - Create a **commit** in your Git repository that includes the iteration status and your **self-assessed score** for **this iteration only**, out of **40 points**. 
   - To receive the **maximum points**, your code must **work as intended**, and run **without crashing**.     
   - **Example** *commit message*:  
     ```  
     [iteration 5]: grade 20 out of 40 points
     ```  
   - Push the updated code to your GitHub repository.
   - **Important:** Failure to push commits may result in incomplete grading.
