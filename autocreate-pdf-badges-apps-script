function autoFillFromSheet() {
  //Base Sheet
  var ss = SpreadsheetApp.openById("XXXXXXXXXXXXXXXXXXXXXXXXXX");
  var sheet = ss.getSheetByName('Names');
  var nameRange = sheet.getRange("A2:B82").getValues();
  //Template Document
  var templateFile =  DriveApp.getFileById('XXXXXXXXXXXXXXXXXXXXXXXXXX');
  var templateFileId = templateFile.getId();
  //Target Folder
  var targetFolderId = DriveApp.getFolderById('XXXXXXXXXXXXXXXXXXXXXXXXXX');
  //Autofill and Create PDFs
  for(var i = 0; i < nameRange.length; i++){
    var row = nameRange[i];
    var copyDoc = templateFile.makeCopy();
    var copyDocId = copyDoc.getId();
    var copyDocOpen = DocumentApp.openById(copyDocId);
    DriveApp.getFileById(copyDocId).setName('NAME_' + row[0] + '_' + row[1]);
    var body = DocumentApp.openById(copyDocId).getBody();
    body.replaceText("##FIRST##", row[0]);
    body.replaceText("##LAST##", row[1]);
    copyDocOpen.saveAndClose();
    var newPdf = DriveApp.createFile(copyDocOpen.getAs('application/pdf'));
    newPdf.setName('NAME_' + row[0] + '_' + row[1]);
    targetFolderId.addFile(newPdf);
    DriveApp.getRootFolder().removeFile(newPdf);
    copyDoc.setTrashed(true)
  }
}
