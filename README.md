Lightning Web Components and Salesforce Data 
Use Lightning Data Service to Work with Data :


contactCreator.html: 
<template>
    <lightning-card>
        <lightning-record-form
            object-api-name={objectApiName}
            fields={fields}
            onsuccess={handleSuccess}>
        </lightning-record-form>
    </lightning-card>
</template>

contactCreator.js:

import { LightningElement } from 'lwc';
import { ShowToastEvent } from 'lightning/platformShowToastEvent';
import CONTACT_OBJECT from '@salesforce/schema/Contact';
import LASTNAME_FIELD from '@salesforce/schema/contact.LastName';
import FIRSTNAME_FIELD from '@salesforce/schema/Contact.FirstName';
import EMAIL_FIELD from '@salesforce/schema/Contact.Email';
export default class contactCreator extends LightningElement {
    objectApiName = CONTACT_OBJECT;
    fields = [LASTNAME_FIELD, FIRSTNAME_FIELD, EMAIL_FIELD];
    handleSuccess(event) {
        const toastEvent = new ShowToastEvent({
            title: "Account created",
            message: "Record ID: " + event.detail.id,
            variant: "success"
        });
        this.dispatchEvent(toastEvent);
    }
}


contactCreator.js-meta.xml:


<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <isExposed>true</isExposed>
    <targets>
        <target>lightning__AppPage</target>
    </targets>
</LightningComponentBundle>
