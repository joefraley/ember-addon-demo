# ReadMe

## Results

See live demo at [codesanbox](https://codesandbox.io/s/github/joefraley/ember-addon-demo)
```sh
git clone https://github.com/joefraley/ember-addon-demo.git
cd ember-addon-demo
yarn
...
yarn start
open http://localhost:4676/
```

~[](https://www.evernote.com/l/AcQDpVct2opBw7r4WSPmXuUZ7VZVTpK_6wEB/image.png)

## Structure

Created by...

```sh
npm install -g ember-cli
ember -v 3.9.0
ember ember-addon-demo
mkdir ember-addon-demo/packages
ember addon component-library
mv component-library ember-addon-demo/packages
# setup yarn workspace for ember-addon-demo
# as described here: https://github.com/habdelra/yarn-workface/tree/master/packages/tomorrow
# ...
# ...
cd ember-addon-demo/packages/component-library
ember generate component button --pod
# fill in the component code...
```

```sh
app/
  templates/
    application.hbs
packages/
  component-library-addon/
    addon/
      components/
        button/
          component.js
          template.hbs
          styles.scss
    app/
      components/
        button/
          component.js <--- re-export
```

```js
// ./packages/betterup-component-library/addon/components/button/component.js
import Component from '@ember/component';
import hbs from 'htmlbars-inline-precompile';
import { tagName, layout } from '@ember-decorators/component';

@tagName('')
@layout(hbs`
<button class="{{styleNamespace}} {{kind}} {{size}}" onClick={{@onClick}} >
  {{yield}}
</button>`)
export default class Button extends Component {
  kind = "primary"
  size = "medium"
}
```

```scss
// ./packages/betterup-component-library/addon/components/button/styles.scss
&.primary {
  background: hotpink;
}
```

```hbs
<!-- ./app/templates/application.hbs -->
<Button kind="primary" size="medium">Click Me</Button>
```