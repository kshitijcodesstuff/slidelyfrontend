Below is the file structure for the Visual Basic desktop application along with the code for each file.

### File Structure

```
SlidelyApp/
├── ApiClient.vb
├── CreateSubmissionForm.Designer.vb
├── CreateSubmissionForm.vb
├── CreateSubmissionForm.resx
├── MainForm.Designer.vb
├── MainForm.vb
├── MainForm.resx
├── My Project/
│   ├── Application.Designer.vb
│   ├── Application.myapp
│   ├── AssemblyInfo.vb
│   ├── Resources.Designer.vb
│   ├── Resources.resx
│   └── Settings.Designer.vb
│   └── Settings.settings
├── Submission.vb
├── ViewSubmissionsForm.Designer.vb
├── ViewSubmissionsForm.vb
└── ViewSubmissionsForm.resx
```

### Code for Each File

#### `ApiClient.vb`
```vb
Imports System.Net
Imports Newtonsoft.Json

Public Class ApiClient
    Private Shared baseUrl As String = "http://localhost:3000/api"

    Public Shared Function GetSubmissions() As List(Of Submission)
        Using client As New WebClient()
            Dim json As String = client.DownloadString($"{baseUrl}/read")
            Return JsonConvert.DeserializeObject(Of List(Of Submission))(json)
        End Using
    End Function

    Public Shared Sub SubmitForm(submission As Submission)
        Using client As New WebClient()
            client.Headers(HttpRequestHeader.ContentType) = "application/json"
            Dim data As String = JsonConvert.SerializeObject(submission)
            client.UploadString($"{baseUrl}/submit", "POST", data)
        End Using
    End Sub
End Class
```

#### `Submission.vb`
```vb
Public Class Submission
    Public Property Name As String
    Public Property Email As String
    Public Property Phone As String
    Public Property GitHubLink As String
    Public Property StopwatchTime As String
End Class
```

#### `MainForm.Designer.vb`
```vb
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _
Partial Class MainForm
    Inherits System.Windows.Forms.Form

    Private Sub InitializeComponent()
        Me.btnViewSubmissions = New System.Windows.Forms.Button()
        Me.btnCreateNewSubmission = New System.Windows.Forms.Button()
        Me.SuspendLayout()
        '
        'btnViewSubmissions
        '
        Me.btnViewSubmissions.Location = New System.Drawing.Point(12, 12)
        Me.btnViewSubmissions.Name = "btnViewSubmissions"
        Me.btnViewSubmissions.Size = New System.Drawing.Size(160, 23)
        Me.btnViewSubmissions.TabIndex = 0
        Me.btnViewSubmissions.Text = "View Submissions (&V)"
        Me.btnViewSubmissions.UseVisualStyleBackColor = True
        '
        'btnCreateNewSubmission
        '
        Me.btnCreateNewSubmission.Location = New System.Drawing.Point(12, 41)
        Me.btnCreateNewSubmission.Name = "btnCreateNewSubmission"
        Me.btnCreateNewSubmission.Size = New System.Drawing.Size(160, 23)
        Me.btnCreateNewSubmission.TabIndex = 1
        Me.btnCreateNewSubmission.Text = "Create New Submission (&C)"
        Me.btnCreateNewSubmission.UseVisualStyleBackColor = True
        '
        'MainForm
        '
        Me.ClientSize = New System.Drawing.Size(284, 261)
        Me.Controls.Add(Me.btnCreateNewSubmission)
        Me.Controls.Add(Me.btnViewSubmissions)
        Me.Name = "MainForm"
        Me.Text = "SlidelyApp"
        Me.ResumeLayout(False)

    End Sub

    Friend WithEvents btnViewSubmissions As Button
    Friend WithEvents btnCreateNewSubmission As Button
End Class
```

#### `MainForm.vb`
```vb
Public Class MainForm
    Private Sub btnViewSubmissions_Click(sender As Object, e As EventArgs) Handles btnViewSubmissions.Click
        Dim viewForm As New ViewSubmissionsForm()
        viewForm.ShowDialog()
    End Sub

    Private Sub btnCreateNewSubmission_Click(sender As Object, e As EventArgs) Handles btnCreateNewSubmission.Click
        Dim createForm As New CreateSubmissionForm()
        createForm.ShowDialog()
    End Sub
End Class
```

#### `CreateSubmissionForm.Designer.vb`
```vb
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _
Partial Class CreateSubmissionForm
    Inherits System.Windows.Forms.Form

    Private Sub InitializeComponent()
        Me.txtName = New System.Windows.Forms.TextBox()
        Me.txtEmail = New System.Windows.Forms.TextBox()
        Me.txtPhone = New System.Windows.Forms.TextBox()
        Me.txtGitHub = New System.Windows.Forms.TextBox()
        Me.lblStopwatchTime = New System.Windows.Forms.Label()
        Me.btnStartStop = New System.Windows.Forms.Button()
        Me.btnSubmit = New System.Windows.Forms.Button()
        Me.SuspendLayout()
        '
        'txtName
        '
        Me.txtName.Location = New System.Drawing.Point(12, 12)
        Me.txtName.Name = "txtName"
        Me.txtName.Size = New System.Drawing.Size(260, 20)
        Me.txtName.TabIndex = 0
        '
        'txtEmail
        '
        Me.txtEmail.Location = New System.Drawing.Point(12, 38)
        Me.txtEmail.Name = "txtEmail"
        Me.txtEmail.Size = New System.Drawing.Size(260, 20)
        Me.txtEmail.TabIndex = 1
        '
        'txtPhone
        '
        Me.txtPhone.Location = New System.Drawing.Point(12, 64)
        Me.txtPhone.Name = "txtPhone"
        Me.txtPhone.Size = New System.Drawing.Size(260, 20)
        Me.txtPhone.TabIndex = 2
        '
        'txtGitHub
        '
        Me.txtGitHub.Location = New System.Drawing.Point(12, 90)
        Me.txtGitHub.Name = "txtGitHub"
        Me.txtGitHub.Size = New System.Drawing.Size(260, 20)
        Me.txtGitHub.TabIndex = 3
        '
        'lblStopwatchTime
        '
        Me.lblStopwatchTime.AutoSize = True
        Me.lblStopwatchTime.Location = New System.Drawing.Point(12, 113)
        Me.lblStopwatchTime.Name = "lblStopwatchTime"
        Me.lblStopwatchTime.Size = New System.Drawing.Size(49, 13)
        Me.lblStopwatchTime.TabIndex = 4
        Me.lblStopwatchTime.Text = "00:00:00"
        '
        'btnStartStop
        '
        Me.btnStartStop.Location = New System.Drawing.Point(12, 129)
        Me.btnStartStop.Name = "btnStartStop"
        Me.btnStartStop.Size = New System.Drawing.Size(75, 23)
        Me.btnStartStop.TabIndex = 5
        Me.btnStartStop.Text = "Start"
        Me.btnStartStop.UseVisualStyleBackColor = True
        '
        'btnSubmit
        '
        Me.btnSubmit.Location = New System.Drawing.Point(197, 129)
        Me.btnSubmit.Name = "btnSubmit"
        Me.btnSubmit.Size = New System.Drawing.Size(75, 23)
        Me.btnSubmit.TabIndex = 6
        Me.btnSubmit.Text = "Submit"
        Me.btnSubmit.UseVisualStyleBackColor = True
        '
        'CreateSubmissionForm
        '
        Me.ClientSize = New System.Drawing.Size(284, 161)
        Me.Controls.Add(Me.btnSubmit)
        Me.Controls.Add(Me.btnStartStop)
        Me.Controls.Add(Me.lblStopwatchTime)
        Me.Controls.Add(Me.txtGitHub)
        Me.Controls.Add(Me.txtPhone)
        Me.Controls.Add(Me.txtEmail)
        Me.Controls.Add(Me.txtName)
        Me.Name = "CreateSubmissionForm"
        Me.Text = "Create New Submission"
        Me.ResumeLayout(False)
        Me.PerformLayout()

    End Sub

    Friend WithEvents txtName As TextBox
    Friend WithEvents txtEmail As TextBox
    Friend WithEvents txtPhone As TextBox
    Friend WithEvents txtGitHub As TextBox
    Friend WithEvents lblStopwatchTime As Label
    Friend WithEvents btnStartStop As Button
    Friend WithEvents btnSubmit As Button
End Class
```

#### `CreateSubmissionForm.vb`
```vb
Public Class CreateSubmissionForm
    Private stopwatch As New Stopwatch()

    Private Sub btnStartStop_Click(sender As Object, e As EventArgs) Handles btnStartStop.Click
        If stopwatch.IsRunning Then
            stopwatch.Stop()
            btnStartStop.Text = "Resume"
        Else
            stopwatch.Start()
            btnStartStop.Text = "Pause"
        End If
        lblStopwatchTime.Text = stopwatch.Elapsed.ToString("hh\:mm\:ss")
    End Sub

    Private Sub btnSubmit_Click(sender As Object, e As EventArgs) Handles btnSubmit.Click
        Dim submission As New Submission With {
            .Name = txtName.Text,
            .Email = txtEmail.Text,
            .Phone = txtPhone.Text,
            .GitHubLink = txtGitHub.Text,
            .StopwatchTime = lblStopwatchTime.Text
        }

        ApiClient.SubmitForm(submission)
        MessageBox.Show("Submission successful!")
        Me.Close()
    End Sub

    Private Sub CreateSubmissionForm_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        Me.KeyPreview = True
    End Sub

    Private Sub CreateSubmissionForm_KeyDown(sender As Object, e As KeyEventArgs) Handles MyBase.KeyDown
        If e.Control AndAlso e.KeyCode =

 Keys.S Then
            btnSubmit.PerformClick()
        End If
    End Sub
End Class
```

#### `ViewSubmissionsForm.Designer.vb`
```vb
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _
Partial Class ViewSubmissionsForm
    Inherits System.Windows.Forms.Form

    Private Sub InitializeComponent()
        Me.dgvSubmissions = New System.Windows.Forms.DataGridView()
        CType(Me.dgvSubmissions, System.ComponentModel.ISupportInitialize).BeginInit()
        Me.SuspendLayout()
        '
        'dgvSubmissions
        '
        Me.dgvSubmissions.ColumnHeadersHeightSizeMode = System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode.AutoSize
        Me.dgvSubmissions.Location = New System.Drawing.Point(12, 12)
        Me.dgvSubmissions.Name = "dgvSubmissions"
        Me.dgvSubmissions.Size = New System.Drawing.Size(760, 437)
        Me.dgvSubmissions.TabIndex = 0
        '
        'ViewSubmissionsForm
        '
        Me.ClientSize = New System.Drawing.Size(784, 461)
        Me.Controls.Add(Me.dgvSubmissions)
        Me.Name = "ViewSubmissionsForm"
        Me.Text = "View Submissions"
        CType(Me.dgvSubmissions, System.ComponentModel.ISupportInitialize).EndInit()
        Me.ResumeLayout(False)

    End Sub

    Friend WithEvents dgvSubmissions As DataGridView
End Class
```

#### `ViewSubmissionsForm.vb`
```vb
Public Class ViewSubmissionsForm
    Private Sub ViewSubmissionsForm_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        Dim submissions As List(Of Submission) = ApiClient.GetSubmissions()
        dgvSubmissions.DataSource = submissions
    End Sub
End Class
```

### My Project

The `My Project` directory contains files that are automatically generated by Visual Studio and manage application settings, resources, and assembly information.

#### `Application.Designer.vb`
This file is automatically generated and usually doesn't require manual editing.

#### `Application.myapp`
This file contains application-level settings.

#### `AssemblyInfo.vb`
This file contains metadata about the assembly.

#### `Resources.Designer.vb` and `Resources.resx`
These files manage application resources like strings, images, and icons.

#### `Settings.Designer.vb` and `Settings.settings`
These files manage user settings.

### Running the Desktop Application

1. Open the `SlidelyApp` project in Visual Studio.
2. Ensure that the `Newtonsoft.Json` NuGet package is installed.
3. Build and run the project.

The application should open a main form with options to create a new submission or view existing submissions. The create form includes a stopwatch feature, and the view form displays submissions in a DataGridView.