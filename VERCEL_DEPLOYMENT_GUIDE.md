# Vercel Deployment Guide (Frontend Only)

Your UCC Dashboard is now ready for deployment. Since the system uses a real-time **Socket.io** backend, the deployment is split into two parts.

## 1. Deploy the Frontend to Vercel
1. Push your code to a GitHub repository.
2. Go to [Vercel](https://vercel.com) and click **Add New > Project**.
3. Select your repository.
4. **IMPORTANT**: Set the **Root Directory** to `nist-5g-dashboard`. 
   > [!WARNING]
   > If you do not set the Root Directory, Vercel will try to deploy the entire folder and will FAIL because of the backend code.
5. Add the following **Environment Variables**:
   - `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`: `AIzaSyAJwO038i9e_E_B0Qsl9CYiidurI_B_vNQ`
   - `NEXT_PUBLIC_API_URL`: Use your hosted backend URL (e.g., `https://your-backend.azurewebsites.net`)
6. Click **Deploy**.

## 2. Deploy the Backend
Vercel does **not** support long-running Express/Socket.io servers. You should maintain the backend deployment on **Azure** (as previously configured) or use a service like **Railway** or **Render**.

### Why split the deployment?
- **Vercel**: Optimized for static assets and Next.js frontend performance.
- **Azure/Railway**: Optimized for persistent database connections and WebSocket (Real-time) data.

---

### Dashboard Fixes Applied
- [x] **Resolved Hydration Error**: Fixed the `validateDOMNesting` error in the AI Assistant (was using a `<div>` inside a `<p>`).
- [x] **Vercel Optimizations**: Added `vercel.json` to ensure correct build settings.
