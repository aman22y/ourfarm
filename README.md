<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cow & Buffalo Master — Smart Registry (Add Fix)</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;700&display=swap" rel="stylesheet">
  <style>
    /* (Styles remain the same as previous version for brevity; copy from history if needed) */
    :root {
      --main: #6366f1;
      --main-dark: #3730a3;
      --text-main: #171717;
      --surface: #ffffff;
      --bg: #f4f6fc;
      --border: #d1d5db;
      --accent: #a5b4fc;
      --error: #ef4444;
      --radius: 10px;
    }
    body {
      font-family: 'Manrope', Arial, sans-serif;
      margin: 0;
      background: var(--bg);
      color: var(--text-main);
      letter-spacing: 0.01em;
      font-size: 0.95em;
    }
    .sticky-search {
      position: sticky;
      top: 0;
      z-index: 5;
      background: var(--bg);
      padding: 8px 15px 2px 15px;
      border-bottom: 1px solid var(--border);
      box-shadow: 0 1px 4px #edefff66;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .sticky-search input {
      flex: 1;
      padding: 8px 10px;
      border-radius: var(--radius);
      border: 1px solid var(--accent);
      font-size: 1em;
    }
    .action-btn {
      background: var(--main);
      border: none;
      color: #fff;
      border-radius: 6px;
      padding: 6px 10px;
      font-size: 0.9em;
      cursor: pointer;
      font-weight: 600;
      transition: background 0.22s;
    }
    .action-btn:hover { background: var(--main-dark); }
    .main-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 20px;
      max-width: 1200px;
      margin: 20px auto 0 auto;
      padding: 0 10px;
    }
    .section {
      background: var(--surface);
      padding: 20px 15px 15px 15px;
      border-radius: 16px;
      box-shadow: 0 2px 8px #dbeafe88;
      border-left: 6px solid var(--main);
      min-width: 300px;
      margin-bottom: 4px;
    }
    .section h2 {
      font-size: 18px;
      margin-top: 0;
      color: var(--main-dark);
      letter-spacing: 1px;
      margin-bottom: 12px;
      font-weight: 700;
    }
    .add-btn {
      background: var(--main);
      border: none;
      color: #fff;
      border-radius: 6px;
      padding: 8px 14px;
      font-size: 0.95em;
      margin: 10px 0;
      cursor: pointer;
      font-weight: 600;
      box-shadow: 0 1px 5px #6366f12a;
      transition: background 0.22s;
    }
    .add-btn:hover { background: var(--main-dark);}
    .reset-btn {
      background: #ef4444;
      border: none;
      color: #fff;
      border-radius: 6px;
      padding: 8px 14px;
      font-size: 0.95em;
      margin: 10px 0;
      cursor: pointer;
      font-weight: 600;
      transition: background 0.22s;
    }
    .reset-btn:hover { background: #b91c1c;}
    .animal-row {
      display: flex;
      align-items: center;
      width: 100%;
      padding: 6px 0;
      border-bottom: 1px solid var(--border);
      margin: 4px 0;
      flex-wrap: wrap;
    }
    .animal-header {
      display: flex;
      align-items: center;
      flex: 1;
      gap: 10px;
    }
    .animal-header img.profile {
      width: 40px; height: 40px;
      object-fit: cover;
      border-radius: 50%; border: 2px solid var(--main);
      background: #e0e7ff;
    }
    .animal-name { font-size: 1em; font-weight: 700; color: var(--main-dark); }
    .animal-actions button {
      margin-left: 4px;
      padding: 4px 10px;
      font-size: 0.9em;
      border: none;
      border-radius: 4px;
      background: var(--accent);
      color: #233;
      cursor: pointer;
      transition: background 0.19s;
    }
    .animal-actions button:hover { background: var(--main);}
    .collapse-section { margin-top: 6px; width: 100%; }
    .collapse-content { padding: 6px 0 3px 0; }
    .animal-fields label {
      font-size: 0.9em;
      margin-right: 6px;
      color: #484a57;
      font-weight: 500;
      display: block;
      margin-bottom: 2px;
    }
    .animal-fields input, .animal-fields textarea {
      font-size: 0.95em;
      padding: 4px 8px;
      margin: 4px 0;
      border-radius: 5px;
      border: 1px solid var(--border);
      width: 98%;
    }
    .animal-fields input.invalid { border-color: var(--error); }
    .animal-fields textarea { min-height: 36px; width: 98%; }
    .error-msg { color: var(--error); font-size: 0.8em; margin-top: -2px; display: block; }
    .photo-log-entry {
      display: flex; align-items: center; gap: 6px; margin-bottom: 4px;
    }
    .photo-log-entry img { width: 36px; height: 36px; border-radius: 5px; object-fit: cover; border: 1px solid #bbb;}
    .photo-log-entry span { font-size: 12px; color: #555;}
    .history-list { list-style: circle; margin: 2px 0 6px 12px; font-size: 0.9em; color: #444;}
    .history-list li { display: flex; align-items: center; gap: 5px; }
    .history-list input { width: 150px; }
    .history-list button { padding: 2px 6px; font-size: 0.8em; background: var(--accent); border: none; border-radius: 4px; cursor: pointer; }
    .history-list button:hover { background: var(--main); }
    .animal-fields { margin-bottom: 4px; }
    .pregnancy-section { padding-top: 6px; }
    .pregnancy-entry { margin-bottom: 6px; border-bottom: 1px dashed var(--border); padding-bottom: 4px; }
    .pregnancy-entry input, .pregnancy-entry textarea { margin: 2px 0; }
    @media (max-width: 900px) {
      .main-grid { grid-template-columns: 1fr;}
      .section { min-width: unset; }
    }
    @media (max-width: 600px) {
      .section { padding: 10px 5px; }
      .sticky-search { padding: 5px 2vw; font-size: 0.95em; flex-wrap: wrap; gap: 4px; }
      .sticky-search input { flex: 1 1 100%; }
      .action-btn { padding: 4px 8px; font-size: 0.85em; }
      .animal-row { flex-direction: column; align-items: flex-start; }
    }
  </style>
</head>
<body>
<div class="sticky-search">
  <span style="font-weight:bold;color:#6366f1;font-size:1.1em;">🐄 Cow & Buffalo Master</span>
  <input type="search" id="searchInput" placeholder="Search by name, tag, or breed..." onkeyup="searchAnimals()">
  <button class="action-btn" onclick="exportData()">Export</button>
  <label class="action-btn" style="position:relative;">
    Import
    <input type="file" accept=".json" onchange="importData(event)" style="position:absolute;opacity:0;top:0;left:0;width:100%;height:100%;cursor:pointer;">
  </label>
  <button class="action-btn" onclick="clearAllData()" style="background:#ef4444;">Clear</button>
</div>

<div class="main-grid">
  <div class="section" id="cowSection">
    <h2>Cows (Max 50)</h2>
    <div id="cowList"></div>
    <button class="add-btn" onclick="addAnimal('cow', 50)">Add Cow</button>
    <button class="reset-btn" onclick="resetSection('cow')">Reset Section</button>
  </div>

  <div class="section" id="buffaloSection">
    <h2>Buffaloes (Max 50)</h2>
    <div id="buffaloList"></div>
    <button class="add-btn" onclick="addAnimal('buffalo', 50)">Add Buffalo</button>
    <button class="reset-btn" onclick="resetSection('buffalo')">Reset Section</button>
  </div>

  <div class="section" id="calfSection">
    <h2>Calves (Max 25)</h2>
    <div id="calfList"></div>
    <button class="add-btn" onclick="addAnimal('calf', 25)">Add Calf</button>
    <button class="reset-btn" onclick="resetSection('calf')">Reset Section</button>
  </div>

  <div class="section" id="heiferSection">
    <h2>Heifers (Max 25)</h2>
    <div id="heiferList"></div>
    <button class="add-btn" onclick="addAnimal('heifer', 25)">Add Heifer</button>
    <button class="reset-btn" onclick="resetSection('heifer')">Reset Section</button>
  </div>
</div>

<script>
  let animals = { cow: [], buffalo: [], calf: [], heifer: [] };
  let reminders = [];

  window.onload = function () {
    try {
      const saved = localStorage.getItem('animalsData');
      if (saved) {
        animals = JSON.parse(saved);
        console.log('Data loaded successfully from localStorage');
      } else {
        console.log('No saved data found, initializing empty sections');
      }
    } catch (err) {
      console.error('Error loading data from localStorage:', err);
      animals = { cow: [], buffalo: [], calf: [], heifer: [] }; // Reset on error
      alert('Data load error detected. Sections have been reset.');
    }
    ['cow', 'buffalo', 'calf', 'heifer'].forEach(type => {
      if (!Array.isArray(animals[type])) {
        animals[type] = [];
        console.warn(`Fixed missing array for ${type}`);
      }
      renderAnimal(type);
      console.log(`Initialized ${type} section with ${animals[type].length} animals`);
    });
    reloadReminders();
  };

  function saveData() { 
    localStorage.setItem('animalsData', JSON.stringify(animals)); 
    console.log('Data saved to localStorage');
  }

  function resetSection(type) {
    if (!confirm(`Reset ${type} section? This will delete all data in this section.`)) return;
    animals[type] = [];
    saveData();
    renderAnimal(type);
    console.log(`${type} section reset`);
  }

  function addAnimal(type, limit) {
    try {
      if (!Array.isArray(animals[type])) {
        animals[type] = [];
        console.warn(`Initialized missing array for ${type} during add`);
      }
      if (animals[type].length >= limit) {
        alert("Limit reached for " + type);
        console.log(`Add failed: Limit reached for ${type} (${animals[type].length}/${limit})`);
        return;
      }
      animals[type].forEach(a => { if (a) a.collapsed = true; });
      const id = Date.now();
      animals[type].push({
        id, name: '', breed: '', tag: '', dob: '', weight: '', note: '', photo: '',
        collapsed: false, medicinePhotos: [], semenPhotos: [], semenDates: [], estrusDates: [], pregnancies: []
      });
      saveData();
      renderAnimal(type);
      console.log(`Successfully added animal to ${type}. New total: ${animals[type].length}`);
    } catch (err) {
      console.error(`Error adding to ${type}:`, err);
      alert('Error adding animal. Check console for details.');
    }
  }

  // (Rest of the script remains the same as previous version for brevity; copy from history if needed)
  function toggleDetails(type, id) {
    const a = animals[type].find(a => a.id === id);
    if (a) { a.collapsed = !a.collapsed; saveData(); renderAnimal(type); }
  }

  function renderAnimal(type) {
    const list = document.getElementById(type + 'List');
    if (!list) {
      console.error(`Section ${type} not found in DOM`);
      return;
    }
    let search = document.getElementById('searchInput').value?.toLowerCase() || '';
    list.innerHTML = '';
    animals[type]
      .sort((a, b) => a.name.localeCompare(b.name))
      .forEach((animal, idx) => {
        if (search && ![animal.name, animal.tag, animal.breed].join(' ').toLowerCase().includes(search)) return;
        let medicineImages = animal.medicinePhotos.map(p =>
          `<div class='photo-log-entry'><img src='${p.url}'/><span>${p.time}</span></div>`).join('');
        let semenImages = animal.semenPhotos.map(p =>
          `<div class='photo-log-entry'><img src='${p.url}'/><span>${p.time}</span></div>`).join('');
        let semenList = animal.semenDates.map((date, i) => 
          `<li><input type="datetime-local" value="${date}" onchange="editSemenDate('${type}', ${animal.id}, ${i}, this.value)"><button onclick="deleteSemenDate('${type}', ${animal.id}, ${i})">Delete</button></li>`).join('');
        let estrusList = animal.estrusDates.map((date, i) => 
          `<li><input type="date" value="${date}" onchange="editEstrusDate('${type}', ${animal.id}, ${i}, this.value)"><button onclick="deleteEstrusDate('${type}', ${animal.id}, ${i})">Delete</button></li>`).join('');
        let pregnancyList = animal.pregnancies.map((preg, i) => 
          `<div class="pregnancy-entry">
            <label>Start: <input type="date" value="${preg.start}" onchange="editPregnancy('${type}', ${animal.id}, ${i}, 'start', this.value)"></label>
            <label>Due: <input type="date" value="${preg.due}" onchange="editPregnancy('${type}', ${animal.id}, ${i}, 'due', this.value)"></label>
            <label>Notes: <textarea onchange="editPregnancy('${type}', ${animal.id}, ${i}, 'notes', this.value)">${preg.notes||''}</textarea></label>
            <button onclick="deletePregnancy('${type}', ${animal.id}, ${i})">Delete</button>
          </div>`).join('');
        list.innerHTML += `
          <div class="animal-row" id="${type}-${animal.id}">
            <div class="animal-header">
              <img class="profile" id="preview-${type}-${animal.id}" src="${animal.photo || 'https://via.placeholder.com/40?text=No+Photo'}">
              <div>
                <span class="animal-name">${idx + 1}. ${animal.name || 'Unnamed'} (${animal.tag || ''})</span>
                <span style="font-size:0.9em;color:#686a9e;">${animal.breed||''}${animal.breed?' — ':''}${animal.dob?'DOB: '+animal.dob:''}</span>
              </div>
              <div class="animal-actions" style="margin-left:auto;">
                <button onclick="toggleDetails('${type}', ${animal.id})">${animal.collapsed ? 'Expand' : 'Collapse'}</button>
                <button onclick="removeAnimal('${type}', ${animal.id})">Delete</button>
              </div>
            </div>
            <div class="collapse-section" ${animal.collapsed?'style="display:none"':''}>
              <div class="collapse-content">
                <div class="animal-fields">
                  <label>Name: <input value="${animal.name}" oninput="updateField('${type}', ${animal.id}, 'name', this.value)" placeholder="Name" required></label>
                  <label>Tag: <input value="${animal.tag}" oninput="updateField('${type}', ${animal.id}, 'tag', this.value)" placeholder="Tag Number"></label>
                  <label>Breed: <input value="${animal.breed}" oninput="updateField('${type}', ${animal.id}, 'breed', this.value)" placeholder="Breed"></label>
                  <label>DOB: <input type="date" value="${animal.dob}" oninput="updateField('${type}', ${animal.id}, 'dob', this.value)" ></label>
                  <label>Weight (kg): <input type="number" min="0" value="${animal.weight||''}" oninput="updateField('${type}', ${animal.id}, 'weight', this.value)"></label>
                  <label>Profile Photo: <input type="file" accept="image/*" onchange="previewImage(event, '${type}-${animal.id}', '${type}', ${animal.id})"></label>
                  <label>Notes: <textarea oninput="updateField('${type}', ${animal.id}, 'note', this.value)">${animal.note||''}</textarea></label>
                </div>
                <div style="padding-top:6px;">
                  <b>Medicine/Injection Photos</b>
                  <input type="file" multiple accept="image/*" onchange="uploadMulti(event, '${type}', ${animal.id}, 'medicinePhotos')">
                  <div>${medicineImages||'<span style=color:#aaa;font-size:12px>No medicine record yet</span>'}</div>
                  <b>Semen Photos/Records</b>
                  <input type="file" multiple accept="image/*" onchange="uploadMulti(event, '${type}', ${animal.id}, 'semenPhotos')">
                  <div>${semenImages||'<span style=color:#aaa;font-size:12px>No semen photo yet</span>'}</div>
                  <label>Semen Date: 
                    <input type="datetime-local" onchange="addSemenDate('${type}', ${animal.id}, this.value)">
                  </label>
                  <ul class="history-list">${semenList||'<span style=color:#bbb>No semen dates</span>'}</ul>
                  <label>Estrus (Cycle) Date: 
                    <input type="date" onchange="addEstrusDate('${type}', ${animal.id}, this.value)">
                  </label>
                  <ul class="history-list">${estrusList||'<span style=color:#bbb>No estrus records</span>'}</ul>
                  <div class="pregnancy-section">
                    <b>Pregnancy Tracking</b>
                    <button onclick="addPregnancy('${type}', ${animal.id})">Add Pregnancy</button>
                    <div>${pregnancyList||'<span style=color:#aaa;font-size:12px>No pregnancy records yet</span>'}</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        `;
      });
    console.log(`Rendered ${type} section with ${animals[type].length} animals`);
  }

  function validateField(field, value) {
    if (field === 'name' && !value.trim()) return 'Name is required';
    if (field === 'weight' && (isNaN(value) || value < 0)) return 'Weight must be a positive number';
    if (field === 'dob') {
      const dobDate = new Date(value);
      if (isNaN(dobDate.getTime()) || dobDate > new Date()) return 'Invalid or future DOB';
    }
    return null;
  }

  function updateField(type, id, field, value) {
    const animal = animals[type].find(a => a.id === id);
    if (animal) {
      const error = validateField(field, value);
      if (error) {
        alert(error);
        return;
      }
      animal[field] = value;
      saveData();
      renderAnimal(type);
    }
  }

  function removeAnimal(type, id) {
    if (!confirm('Are you sure you want to delete this animal?')) return;
    animals[type] = animals[type].filter(animal => animal.id !== id);
    saveData();
    renderAnimal(type);
  }

  function previewImage(event, imgId, type, id) {
    const reader = new FileReader();
    reader.onload = function () {
      document.getElementById('preview-' + imgId).src = reader.result;
      const animal = animals[type].find(a => a.id === id);
      if (animal) { animal.photo = reader.result; saveData(); }
    };
    reader.readAsDataURL(event.target.files[0]);
  }

  function uploadMulti(event, type, id, field) {
    const files = event.target.files;
    const animal = animals[type].find(a => a.id === id);
    if (!animal || !files.length) return;
    Array.from(files).forEach(file => {
      const reader = new FileReader();
      reader.onload = function () {
        animal[field].push({ url: reader.result, time: new Date().toLocaleString() });
        saveData(); renderAnimal(type);
      };
      reader.readAsDataURL(file);
    });
  }

  function addSemenDate(type, id, dateTime) {
    const animal = animals[type].find(a => a.id === id);
    if (!animal || !dateTime) return;
    animal.semenDates.push(dateTime);
    saveData();
    renderAnimal(type);
  }

  function editSemenDate(type, id, index, newDate) {
    const animal = animals[type].find(a => a.id === id);
    if (animal && animal.semenDates[index]) {
      animal.semenDates[index] = newDate;
      saveData();
      renderAnimal(type);
    }
  }

  function deleteSemenDate(type, id, index) {
    const animal = animals[type].find(a => a.id === id);
    if (animal) {
      animal.semenDates.splice(index, 1);
      saveData();
      renderAnimal(type);
    }
  }

  function addEstrusDate(type, id, dateStr) {
    const animal = animals[type].find(a => a.id === id);
    if (!animal || !dateStr) return;
    animal.estrusDates.push(dateStr);
    const nextCycle = new Date(dateStr);
    nextCycle.setDate(nextCycle.getDate() + 21);
    const reminderDate = new Date(nextCycle);
    reminderDate.setDate(reminderDate.getDate() - 1);
    const now = new Date();
    const timeUntilReminder = reminderDate.getTime() - now.getTime();
    if (timeUntilReminder > 0) {
      const timeoutId = setTimeout(() => {
        alert(`Reminder: Estrus cycle for "${animal.name || 'animal'}" expected on ${nextCycle.toDateString()}`);
      }, timeUntilReminder);
      reminders.push({ type, id, date: nextCycle.toISOString(), timeoutId });
      localStorage.setItem('reminders', JSON.stringify(reminders));
    }
    saveData();
    renderAnimal(type);
  }

  function editEstrusDate(type, id, index, newDate) {
    const animal = animals[type].find(a => a.id === id);
    if (animal && animal.estrusDates[index]) {
      animal.estrusDates[index] = newDate;
      saveData();
      renderAnimal(type);
    }
  }

  function deleteEstrusDate(type, id, index) {
    const animal = animals[type].find(a => a.id === id);
    if (animal) {
      animal.estrusDates.splice(index, 1);
      saveData();
      renderAnimal(type);
    }
  }

  function addPregnancy(type, id) {
    const animal = animals[type].find(a => a.id === id);
    if (!animal) return;
    animal.pregnancies.push({ start: '', due: '', notes: '' });
    saveData();
    renderAnimal(type);
  }

  function editPregnancy(type, id, index, field, value) {
    const animal = animals[type].find(a => a.id === id);
    if (animal && animal.pregnancies[index]) {
      animal.pregnancies[index][field] = value;
      saveData();
      renderAnimal(type);
    }
  }

  function deletePregnancy(type, id, index) {
    const animal = animals[type].find(a => a.id === id);
    if (animal) {
      animal.pregnancies.splice(index, 1);
      saveData();
      renderAnimal(type);
    }
  }

  function searchAnimals() {
    ['cow', 'buffalo', 'calf', 'heifer'].forEach(type => renderAnimal(type));
  }

  function exportData() {
    const dataStr = JSON.stringify(animals);
    const blob = new Blob([dataStr], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'animals-data.json';
    a.click();
    URL.revokeObjectURL(url);
  }

  function importData(event) {
    const file = event.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = function (e) {
      try {
        const imported = JSON.parse(e.target.result);
        Object.assign(animals, imported);
        saveData();
        ['cow', 'buffalo', 'calf', 'heifer'].forEach(type => renderAnimal(type));
        alert('Data imported successfully!');
        reloadReminders();
      } catch (err) {
        alert('Invalid file or data format.');
        console.error('Import error:', err);
      }
    };
    reader.readAsText(file);
  }

  function clearAllData() {
    if (!confirm('Are you sure? This will delete all data permanently.')) return;
    localStorage.clear();
    animals = { cow: [], buffalo: [], calf: [], heifer: [] };
    reminders.forEach(r => clearTimeout(r.timeoutId));
    reminders = [];
    ['cow', 'buffalo', 'calf', 'heifer'].forEach(type => renderAnimal(type));
  }

  function reloadReminders() {
    reminders = JSON.parse(localStorage.getItem('reminders')) || [];
    reminders.forEach(r => {
      const now = new Date();
      const reminderDate = new Date(r.date);
      const timeUntil = reminderDate.getTime() - now.getTime();
      if (timeUntil > 0) {
        r.timeoutId = setTimeout(() => {
          const animal = animals[r.type].find(a => a.id === r.id);
          if (animal) {
            alert(`Reminder: Estrus cycle for "${animal.name || 'animal'}" expected on ${reminderDate.toDateString()}`);
          }
        }, timeUntil);
      }
    });
  }
</script>
</body>
</html>
