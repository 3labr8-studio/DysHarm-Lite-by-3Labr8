# Building the VST3

The current Visual Studio solution was generated when the project was a **standalone app**. It only contains the **"App"** target, which builds an `.exe` — **no VST3 is produced** when you build that.

To get a **VST3** you must **re-export the project from the Projucer** so it creates a proper plugin solution with a VST3 target.

---

## Step 1: Open the project in Projucer

1. Open **Projucer** (from your JUCE installation).
2. **File → Open** and select:
   ```
   Dys-Harm Lite by 3Labr8.jucer
   ```
   (in the project root folder).

---

## Step 2: Fix JUCE path (if you get "cannot open file" or path errors)

If you see many errors about missing files or `JUCE\modules\...`:

1. In Projucer: **File → Global Paths** (or **Projucer → Global Paths** on Mac).
2. Set **JUCE path** to the folder that **contains** the `modules` folder.
   - Example: `C:\Users\YourName\JUCE`  
     (so that `C:\Users\YourName\JUCE\modules` exists).
3. Click **Save** and close the dialog.

---

## Step 3: Regenerate the solution (creates the VST3 target)

1. In Projucer, click **Save Project and Open in IDE**  
   (or **File → Save Project**, then open the solution yourself).
2. This **overwrites** the existing `.sln` and `.vcxproj` files and creates:
   - A **VST3** target (builds the `.vst3` plugin).
   - Possibly a **Standalone** target (builds the host app), depending on export settings.

---

## Step 4: Build the VST3

1. Open the **regenerated** solution in Visual Studio (e.g. `Builds/VisualStudio2017/Dys-Harm Lite by 3Labr8.sln`).
2. In the **Solution Configuration** dropdown, choose **Release** (or **Debug** if you prefer).
3. In the **Solution Explorer**, find the project named like **"Dys-Harm Lite by 3Labr8 - VST3"** (or similar).
4. **Right‑click that project → Set as Startup Project** (optional).
5. **Build → Build Solution** (or build only the VST3 project).
6. The built **.vst3** will be in the output folder, e.g.:
   ```
   Builds\VisualStudio2017\x64\Release\VST3\Dys-Harm Lite by 3Labr8.vst3
   ```
   (exact path may vary; check the project’s **Output** path in the IDE.)

---

## Step 5: Install the VST3 (optional)

Copy the **entire** `.vst3` folder (e.g. `Dys-Harm Lite by 3Labr8.vst3`) to your host’s VST3 folder, for example:

- **Windows:** `C:\Program Files\Common Files\VST3`
- Or the path your DAW uses for VST3 plugins.

Rescan plugins in your DAW so it picks up the new VST3.

---

## If you still get errors after re-exporting

- **"Cannot open include file" / path errors**  
  Fix the **JUCE path** in Projucer (Step 2) and **Save Project and Open in IDE** again.

- **Link errors / unresolved symbols**  
  Make sure you built the **VST3** project, not only the App/Standalone project.

- **Projucer says "outdated Projucer"**  
  Update JUCE (or the Projucer app) so it matches the JUCE version in your project, then re-save the project.

- **No "VST3" project in the solution**  
  In Projucer, check **Plugin Formats** and ensure **VST3** is enabled, then **Save Project and Open in IDE** again.
