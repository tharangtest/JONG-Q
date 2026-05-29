[queue.html](https://github.com/user-attachments/files/28381845/queue.html)

<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Graphic Queue System</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Prompt', sans-serif;
    }

    body {
      background: #0f172a;
      color: white;
      min-height: 100vh;
      padding: 30px;
    }

    .container {
      max-width: 1300px;
      margin: auto;
    }

    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 30px;
      flex-wrap: wrap;
      gap: 15px;
    }

    .title {
      font-size: 32px;
      font-weight: 700;
    }

    .subtitle {
      color: #94a3b8;
      margin-top: 5px;
    }

    .stats {
      display: flex;
      gap: 15px;
      flex-wrap: wrap;
      margin-bottom: 25px;
    }

    .card {
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 20px;
      padding: 20px;
      backdrop-filter: blur(10px);
      flex: 1;
      min-width: 180px;
    }

    .card h3 {
      color: #94a3b8;
      font-size: 14px;
      margin-bottom: 8px;
      font-weight: 400;
    }

    .card .number {
      font-size: 34px;
      font-weight: 700;
    }

    .layout {
      display: grid;
      grid-template-columns: 350px 1fr;
      gap: 25px;
    }

    .panel {
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 24px;
      padding: 25px;
      backdrop-filter: blur(10px);
    }

    .panel h2 {
      margin-bottom: 20px;
      font-size: 22px;
    }

    .form-group {
      margin-bottom: 18px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      color: #cbd5e1;
      font-size: 14px;
    }

    input,
    select,
    textarea {
      width: 100%;
      padding: 14px;
      border-radius: 14px;
      border: none;
      outline: none;
      background: rgba(255,255,255,0.08);
      color: white;
      font-size: 14px;
    }

    select option {
      color: black;
    }

    textarea {
      resize: none;
      height: 100px;
    }

    .btn {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 14px;
      background: linear-gradient(135deg, #f97316, #fb7185);
      color: white;
      font-size: 15px;
      font-weight: 600;
      cursor: pointer;
      transition: 0.3s;
    }

    .btn:hover {
      transform: translateY(-2px);
      opacity: 0.95;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th {
      text-align: left;
      padding-bottom: 15px;
      color: #94a3b8;
      font-size: 14px;
      font-weight: 400;
    }

    td {
      padding: 16px 10px;
      border-top: 1px solid rgba(255,255,255,0.08);
      font-size: 14px;
    }

    .badge {
      padding: 7px 12px;
      border-radius: 999px;
      font-size: 12px;
      font-weight: 600;
      display: inline-block;
    }

    .high {
      background: rgba(239,68,68,0.2);
      color: #fca5a5;
    }

    .medium {
      background: rgba(245,158,11,0.2);
      color: #fcd34d;
    }

    .low {
      background: rgba(34,197,94,0.2);
      color: #86efac;
    }

    .waiting {
      background: rgba(59,130,246,0.2);
      color: #93c5fd;
    }

    .working {
      background: rgba(168,85,247,0.2);
      color: #d8b4fe;
    }

    .done {
      background: rgba(34,197,94,0.2);
      color: #86efac;
    }

    .action-btn {
      border: none;
      padding: 8px 12px;
      border-radius: 10px;
      cursor: pointer;
      font-size: 12px;
      margin-right: 5px;
      color: white;
    }

    .edit-btn {
      background: #3b82f6;
    }

    .delete-btn {
      background: #ef4444;
    }

    .empty {
      text-align: center;
      color: #94a3b8;
      padding: 40px;
    }

    @media(max-width: 980px) {
      .layout {
        grid-template-columns: 1fr;
      }

      .table-wrapper {
        overflow-x: auto;
      }

      table {
        min-width: 800px;
      }
    }
  </style>
</head>
<body>
  <div class="container">

    <div class="header">
      <div>
        <div class="title">🎨 Graphic Design Queue</div>
        <div class="subtitle">ระบบจัดคิวงานกราฟิกสำหรับทีมดีไซน์</div>
      </div>
    </div>

    <div class="stats">
      <div class="card">
        <h3>งานทั้งหมด</h3>
        <div class="number" id="totalJobs">0</div>
      </div>

      <div class="card">
        <h3>รอทำ</h3>
        <div class="number" id="waitingJobs">0</div>
      </div>

      <div class="card">
        <h3>กำลังทำ</h3>
        <div class="number" id="workingJobs">0</div>
      </div>

      <div class="card">
        <h3>เสร็จแล้ว</h3>
        <div class="number" id="doneJobs">0</div>
      </div>
    </div>

    <div class="layout">

      <div class="panel">
        <h2>➕ เพิ่มคิวงาน</h2>

        <div class="form-group">
          <label>ชื่องาน</label>
          <input type="text" id="jobName" placeholder="เช่น Banner HONOR 600">
        </div>

        <div class="form-group">
          <label>ผู้ส่งงาน</label>
          <input type="text" id="sender" placeholder="ชื่อผู้ส่งงาน">
        </div>

        <div class="form-group">
          <label>Deadline</label>
          <input type="date" id="deadline">
        </div>

        <div class="form-group">
          <label>ความด่วน</label>
          <select id="priority">
            <option value="สูง">สูง</option>
            <option value="กลาง">กลาง</option>
            <option value="ต่ำ">ต่ำ</option>
          </select>
        </div>

        <div class="form-group">
          <label>รายละเอียดงาน</label>
          <textarea id="detail" placeholder="รายละเอียดเพิ่มเติม"></textarea>
        </div>

        <button class="btn" onclick="addJob()">เพิ่มคิวงาน</button>
      </div>

      <div class="panel table-wrapper">
        <h2>📋 ตารางคิวงาน</h2>

        <table>
          <thead>
            <tr>
              <th>คิว</th>
              <th>ชื่องาน</th>
              <th>ผู้ส่ง</th>
              <th>Deadline</th>
              <th>Priority</th>
              <th>Status</th>
              <th>จัดการ</th>
            </tr>
          </thead>
          <tbody id="jobTable">
            <tr>
              <td colspan="7" class="empty">ยังไม่มีคิวงาน</td>
            </tr>
          </tbody>
        </table>
      </div>

    </div>
  </div>

  <script>
    let jobs = JSON.parse(localStorage.getItem('graphicJobs')) || [];

    function renderJobs() {
      const table = document.getElementById('jobTable');

      if (jobs.length === 0) {
        table.innerHTML = `
          <tr>
            <td colspan="7" class="empty">ยังไม่มีคิวงาน</td>
          </tr>
        `;
        updateStats();
        return;
      }

      table.innerHTML = '';

      jobs.forEach((job, index) => {
        let priorityClass = '';
        let statusClass = '';

        if(job.priority === 'สูง') priorityClass = 'high';
        if(job.priority === 'กลาง') priorityClass = 'medium';
        if(job.priority === 'ต่ำ') priorityClass = 'low';

        if(job.status === 'รอทำ') statusClass = 'waiting';
        if(job.status === 'กำลังทำ') statusClass = 'working';
        if(job.status === 'เสร็จแล้ว') statusClass = 'done';

        table.innerHTML += `
          <tr>
            <td>#${String(index + 1).padStart(3, '0')}</td>
            <td>
              <strong>${job.name}</strong><br>
              <small style="color:#94a3b8">${job.detail}</small>
            </td>
            <td>${job.sender}</td>
            <td>${job.deadline}</td>
            <td><span class="badge ${priorityClass}">${job.priority}</span></td>
            <td>
              <select onchange="changeStatus(${index}, this.value)">
                <option ${job.status === 'รอทำ' ? 'selected' : ''}>รอทำ</option>
                <option ${job.status === 'กำลังทำ' ? 'selected' : ''}>กำลังทำ</option>
                <option ${job.status === 'เสร็จแล้ว' ? 'selected' : ''}>เสร็จแล้ว</option>
              </select>
            </td>
            <td>
              <button class="action-btn delete-btn" onclick="deleteJob(${index})">ลบ</button>
            </td>
          </tr>
        `;
      });

      updateStats();
      saveData();
    }

    function addJob() {
      const name = document.getElementById('jobName').value;
      const sender = document.getElementById('sender').value;
      const deadline = document.getElementById('deadline').value;
      const priority = document.getElementById('priority').value;
      const detail = document.getElementById('detail').value;

      if (!name || !sender || !deadline) {
        alert('กรุณากรอกข้อมูลให้ครบ');
        return;
      }

      jobs.push({
        name,
        sender,
        deadline,
        priority,
        detail,
        status: 'รอทำ'
      });

      document.getElementById('jobName').value = '';
      document.getElementById('sender').value = '';
      document.getElementById('deadline').value = '';
      document.getElementById('detail').value = '';

      renderJobs();
    }

    function deleteJob(index) {
      if(confirm('ต้องการลบคิวนี้หรือไม่?')) {
        jobs.splice(index, 1);
        renderJobs();
      }
    }

    function changeStatus(index, status) {
      jobs[index].status = status;
      saveData();
      updateStats();
    }

    function updateStats() {
      document.getElementById('totalJobs').innerText = jobs.length;
      document.getElementById('waitingJobs').innerText = jobs.filter(j => j.status === 'รอทำ').length;
      document.getElementById('workingJobs').innerText = jobs.filter(j => j.status === 'กำลังทำ').length;
      document.getElementById('doneJobs').innerText = jobs.filter(j => j.status === 'เสร็จแล้ว').length;
    }

    function saveData() {
      localStorage.setItem('graphicJobs', JSON.stringify(jobs));
    }

    renderJobs();
  </script>
</body>
</html>
