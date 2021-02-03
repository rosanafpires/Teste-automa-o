# Teste-automacao
Teste de automação usando Cypress
/// <reference types="cypress" />

describe('Ongs', () => {
    it('devem poder realizar um cadastro', () => {
        cy.visit('http://localhost:3000/register');
        cy.get('[data-cy=name]').type('Animais Extraordinarios');
        cy.get('[data-cy=email]').type('animais_extraordinarios@mail.com');
        cy.get('[data-cy=whatsapp]').type('51987564455');
        cy.get('[data-cy=city]').type('Porto Alegre');
        cy.get('[data-cy=uf]').type('RS');        
        cy.route('POST', '**/ongs').as('postOng');
        cy.get('[data-cy=submit]').click();
        cy.wait('@postOng').then((xhr) => {
            expect(xhr.status).be.eq(200);
            expect(xhr.response.body).has.property('id');
            expect(xhr.response.body.id).is.not.null;
        });

    });

    it('deve poder realizar um login no sistema', () => {
        cy.visit('http://localhost:3000/');
        cy.get('input').type(Cypress.env('createdOngId'));
        cy.get('.button').click();
    });
}); 
 21  cypress/plugins/index.js 
@@ -0,0 +1,21 @@
/// <reference types="cypress" />
// ***********************************************************
// This example plugins/index.js can be used to load plugins
//
// You can change the location of this file or turn off loading
// the plugins file with the 'pluginsFile' configuration option.
//
// You can read more here:
// https://on.cypress.io/plugins-guide
// ***********************************************************

// This function is called when a project is opened or re-opened (e.g. due to
// the project's config changing)

/**
 * @type {Cypress.PluginConfig}
 */
module.exports = (on, config) => {
  // `on` is used to hook into various events Cypress emits
  // `config` is the resolved Cypress config
}
