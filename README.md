# docker-files
To automate the process of updating a variable array in a Blueprint with assets from a specific directory before packaging, you can create an **Editor Utility Blueprint** that scans a directory and populates the array for you. Here's how to implement this idea:

---

### Step 1: Enable Editor Scripting Utilities
1. Go to **Edit > Plugins**.
2. Under the **Scripting** section, enable the **Editor Scripting Utilities** plugin.
3. Restart Unreal Engine if required.

---

### Step 2: Create an Editor Utility Blueprint
1. Right-click in the Content Browser, go to **Editor Utilities > Editor Utility Blueprint**, and choose **Editor Utility Object**.
2. Name it something like AutoPopulateAssetsUtility.

---

### Step 3: Blueprint Logic to Populate the Array
1. **Get Asset Registry**:
   - Add the Get Asset Registry node to query all assets in a directory.
   
2. **Filter Assets by Type**:
   - Use the Get Assets by Path node with the desired directory (e.g., /Game/MyAssets) and check the **Recursive** option.
   - Use a For Each Loop node to iterate through the assets.
   - Filter the results to include only the type of assets you need (e.g., BlueprintClass, StaticMesh, etc.).

3. **Update the Variable Array**:
   - Create a Variable in your Editor Utility Blueprint (e.g., AssetsArray of type Soft Object Reference or String).
   - Add the filtered assets to this array using the Add or Set nodes.

---

### Step 4: Trigger the Update
1. Add a custom event in the Editor Utility Blueprint (e.g., UpdateAssetsArray) that runs the logic to populate the array.
2. Add a Button to your Editor Utility Widget or call the event from the Blueprint itself.

---

### Step 5: Save the Array to a Blueprint Variable
If you want the populated array to automatically update in your main Blueprint:
1. Add a Variable to your target Blueprint (e.g., StaticMeshArray).
2. From the Editor Utility Blueprint, use the Set node to update this variable in the target Blueprint.

---

### Step 6: Automate the Process
To run the update automatically whenever you add new assets:
1. In the Editor Utility Blueprint, use the Begin Execution event (On Editor Startup or On Clicked) to trigger the UpdateAssetsArray logic.
2. Optionally, bind the event to a hotkey or toolbar button.

---

### Final Notes:
This approach automates the population of your variable array with new assets in a directory and ensures it’s always up to date. Since it happens during the editor phase, the array will be ready before you package your project.
visualize this thanks
