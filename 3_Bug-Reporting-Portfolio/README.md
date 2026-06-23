Bug Reporting Portfolio – Manual Testing

Overview

This portfolio demonstrates a real-world software defect report created during manual testing.
It highlights the ability to identify, document, and structure bugs clearly for developer resolution and QA tracking.

The report follows standard bug tracking practices including severity, priority, reproduction steps, and expected vs actual results.

Bug Summary

Bug ID: #001
Test Case ID: TC PL 001
Reporter: Adakomola Oluwamurewa
Assigned Developer: John Doe
Submit Date: 05/03/2026
Due Date: 15/03/2026

Summary:
The playlist was not automatically marked as downloaded after adding downloaded songs.

Bug Overview

Application Area: Library / Downloaded Section
Platform: Mobile
Operating System: iOS
Browser: Not applicable
Screenshot: Attached in report

Bug Description

When a user creates a new playlist and adds downloaded songs or albums to it, the playlist does not automatically reflect a downloaded status.
This prevents proper offline identification of the playlist.

Steps to Reproduce

Open Spotify
Navigate to Library
Go to Downloaded section
Create a new playlist
Add a downloaded album to the playlist
Add another downloaded album
Open the newly created playlist
Check the download status indicator

Expected Result

The playlist should automatically display as downloaded and be available for offline access.


Actual Result

The playlist does not display as downloaded even after adding downloaded content.


Severity and Priority

Severity: Minor
Priority: Low

Impact

Confusing user experience for offline content management
Incorrect download status indication
No functional crash or data loss


Conclusion

This defect highlights a UI/logic inconsistency in playlist download status tracking.
While not critical, it affects user clarity around offline content and should be addressed in future updates.