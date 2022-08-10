## Properties
- actionPosition,
- actions
- actionSize
- actionMenuIcon

- [ ] Avatar Doc on confluence

## Passing arguments
actionPosition:
check if its in a storybookWrappers!!!
    `avatar.stories.js`
    `/__examples__/avatar.js`
    `avatar.html` -> `action-position={actionPosition}`
    `avatar.js` -> `@api get set`
    `primitiveAvatar.html` -> `action-position={actionPosition}`
    `primitiveAvatar.js` -> `@api get set`


!!! First item is what goes in the documentation on the site

    /**
    * The name of the icon to be used in the format 'utility:down'. For the horizontal variant, if an icon other than 'utility:down' or 'utility:chevrondown' is used, a utility:down icon is appended to the right of that icon.
    *
    * @type {string}
    * @public
    * @default utility:down for horizontal variant
    */
    @api
    get iconName() {
        return this._iconName;
    }
    set iconName(value) {
        this._iconName =
            value && typeof value === 'string'
                ? value.trim()
                : DEFAULT_ICON_NAME;
    }

Ajouter dans confluence!!!

Create test!

storybook wrapper add @api label, variant...

    `primitiveAvatar.html`
    <lightning-button-icon
        size={actionSize}
        icon-name={action.iconName}
        variant="border-filled"
        alternative-text={action.label}
        value={action.name}
        onclick={handleActionClick}
    ></lightning-button-icon>

    `primitiveAvatar.js`
    /**
    * Action clicked event handler.
    *
    * @param {event}
    */
    handleActionClick(event) {
        console.log(event.currentTarget.value);
        /**
        * The event fired when a user clicks on an action.
        *
        * @event
        * @name actionclick
        * @public
        */
        this.dispatchEvent(
            new CustomEvent('actionclick', {
                detail: {
                    name: event.currentTarget.value
                }
            })
        );
    }


    Tests cannot travel to inside inner elements. Avatar cannot test PrimitiveAvatar
    // actions
    it('Avatar with actions', () => {
        const actions = [
            {
                label: 'Edit item',
                name: 'edit-item',
                iconName: 'utility:edit'
            },
            {
                label: 'Add item',
                name: 'add-item',
                iconName: 'utility:add'
            }
        ];
        element.actions = actions;
        element.hideAvatarDetails = true;

        return Promise.resolve().then(() => {
            const avatar = element.shadowRoot.querySelector(
                '[data-element-id="avonni-primitive-avatar-no-details"]'
            );
            expect(avatar.actions).toEqual([
                {
                    label: 'Edit item',
                    name: 'edit-item',
                    iconName: 'utility:edit'
                },
                {
                    label: 'Add item',
                    name: 'add-item',
                    iconName: 'utility:add'
                }
            ]);
        })
    })

### Keep ###
icon-size={actionMenuSize}

avatar size |   menu size
xx-large    |   small
x-large     |   x-small
large       |   x-small (big) xx-small (small)
medium      |   xx-small

show actions if:true={showActions} 
is size small == medium or ... smaller sizes
