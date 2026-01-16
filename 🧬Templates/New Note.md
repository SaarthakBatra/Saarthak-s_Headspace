<%*
// --- CONFIGURATION ---
const vaultId = "5aabe01b2a639311";
// ---------------------

// 1. Prompt for the new file name // Defaults to the current name (e.g., "Untitled") if you hit Esc 
const newName = await tp.system.prompt("Name:", tp.file.title);

// 2. Rename the file if the user entered a name 
if (newName && newName !== tp.file.title) { await tp.file.rename(newName); }

// 3. Get the folder path and split it
const path = tp.file.folder(true);
const folders = path.split("/").filter(f => f !== "/");

// 4. Initialize the breadcrumb trail
let breadcrumbParts = [];
breadcrumbParts.push(`[📁 Explore](obsidian://open?vault=${vaultId}&file=📁%20Explore)`);
        

// 5. Build links: Loop through every folder in the path
const parentNote = (folders[folders.length - 1] === newName)? 1 : 0;

folders.forEach((folderName, index) => {
    const isImmediateParent = (index === folders.length - 1 - parentNote);

	if (folderName === 'Subjects' || folderName === newName) return;
    else if (isImmediateParent) breadcrumbParts.push(`[[${folderName}]]`); // Immediate Parent -> Wiki Link [[ ]]
    else {
        // Ancestors (Grandparents) -> Obsidian URI Link [ ]( )
        // Encodes ' ' to %20 and '&' to %26 as requested
        const encodedName = folderName.replace(/ /g, "%20").replace(/&/g, "%26");
        const uri = `obsidian://open?vault=${vaultId}&file=${encodedName}`;
        
        breadcrumbParts.push(`[${folderName}](${uri})`);
    }
});

// 4. Output the full trail > Current Title
if (breadcrumbParts.length > 0) {
    tR += `${breadcrumbParts.join(" > ")} > ${newName || tp.file.title}`;
} else {
    tR += `${newName || tp.file.title}`;
}
%>

---


---
#incomplete