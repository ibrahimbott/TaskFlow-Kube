# 🎬 Phase 4 Demo Video Script (90 seconds)

## 📋 Pre-Recording Checklist

- [ ] Minikube running
- [ ] Pods deployed and ready
- [ ] Application accessible in browser
- [ ] Terminal ready with commands
- [ ] Browser window clean (close extra tabs)
- [ ] Recording software ready (OBS/Loom/Windows Game Bar)

---

## 🎥 Video Timeline

### **00:00 - 00:15** | Introduction (15 sec)
**Say:**
> "Hello! This is my Phase 4 submission for Hackathon II. I've deployed the Todo AI Chatbot on local Kubernetes using Minikube with Docker."

**Show:**
- Terminal with project directory open
- Quick view of folder structure

---

### **00:15 - 00:35** | Kubernetes Deployment (20 sec)
**Say:**
> "Here you can see the Kubernetes deployment with 4 pods running - 2 frontend replicas and 2 backend replicas for high availability. All pods are healthy and ready."

**Show:**
```powershell
kubectl get pods
kubectl get services
```

**Expected Output:**
```
NAME                            READY   STATUS    RESTARTS   AGE
todo-frontend-xxxxxxxxx-xxxxx   1/1     Running   0          5m
todo-frontend-xxxxxxxxx-xxxxx   1/1     Running   0          5m
todo-backend-xxxxxxxxx-xxxxx    1/1     Running   0          5m
todo-backend-xxxxxxxxx-xxxxx    1/1     Running   0          5m
```

---

### **00:35 - 01:00** | Application Demo (25 sec)
**Say:**
> "Let me demonstrate the AI chatbot. I'll add a task using natural language, then use slash commands for quick actions."

**Show:**
1. **Browser with app open**
2. **Type in chatbot:** "Add a task to prepare hackathon presentation"
3. **Task appears** in the list
4. **Type:** `/list` (show autocomplete)
5. **Tasks displayed**
6. **Type:** `/complete 1`
7. **Task marked as complete**

---

### **01:00 - 01:20** | Technical Features (20 sec)
**Say:**
> "The deployment includes Docker containerization, Helm charts for package management, auto-scaling, health checks, and secrets management for secure configuration."

**Show:**
- Quick switch to terminal
```powershell
# Show Docker images
docker images | Select-String "todo"

# Show Helm chart
ls helm\todo-app\templates
```

---

### **01:20 - 01:30** | Conclusion (10 sec)
**Say:**
> "This demonstrates a production-ready cloud-native deployment following industry best practices. All code is available on GitHub. Thank you!"

**Show:**
- GitHub repository page (optional)
- Or final view of running application

---

## 🎯 Recording Tips

### **Before Recording:**
1. Close unnecessary applications
2. Clear browser history/cache
3. Prepare all commands in a text file
4. Test run once without recording
5. Check audio levels

### **During Recording:**
1. Speak clearly and at moderate pace
2. Don't rush - 90 seconds is enough
3. If you make a mistake, pause and restart
4. Show, don't just tell

### **After Recording:**
1. Watch the full video
2. Check audio quality
3. Verify all features are visible
4. Trim if over 90 seconds
5. Export as MP4 (recommended)

---

## 📤 Upload Options

### **Option 1: YouTube (Unlisted)**
- Upload as "Unlisted" video
- Copy link for submission
- Advantage: No file size limits

### **Option 2: Google Drive**
- Upload MP4 file
- Set sharing to "Anyone with link"
- Copy shareable link
- Advantage: Simple, reliable

### **Option 3: Loom**
- Record directly on Loom
- Auto-generates shareable link
- Advantage: Easiest, no editing needed

---

## ✅ Submission Checklist

After video is ready:

- [ ] Video is under 90 seconds
- [ ] Shows Kubernetes pods running
- [ ] Demonstrates chatbot functionality
- [ ] Shows slash commands
- [ ] Audio is clear
- [ ] Video uploaded and link copied
- [ ] GitHub repo is public
- [ ] README updated with Phase 4 info
- [ ] All code pushed to GitHub

---

## 📋 Submission Form Data

**Form URL:** https://forms.gle/KMKEKaFUD6ZX4UtY8

**What to submit:**
1. **GitHub Repo Link:** https://github.com/YOUR_USERNAME/todo-hackathon
2. **Demo Video Link:** [Your YouTube/Drive/Loom link]
3. **Deployed App Link:** `minikube service todo-frontend --url` (for local)
4. **WhatsApp Number:** Your number for presentation invitation

---

## 🎓 Bonus Points to Mention (If Time)

- "Using Docker multi-stage builds for optimized images"
- "Implemented health checks for automatic pod recovery"
- "Configured resource limits for efficient cluster usage"
- "Following 12-factor app methodology"

---

**Good luck with your demo! 🚀**
