# product-dropdown


  {%- when 'variant_picker' -%}
            
            {% comment %}
              {% render 'product-variant-picker', product: product, block: block, product_form_id: product_form_id %}
           {% endcomment %}
             <!--   variant-option       -->
          {%- unless product.has_only_default_variant -%}
              {%- if block.settings.picker_type == 'button' -%}
        {% comment %}
        {% assign file_extension = "'png', 'jpeg', 'jpg' , 'gif' , 'webp' "%} {% endcomment %}
        {% assign file_extension = "png" %}
                <variant-radios class="no-js-hidden custom-color-list" data-section="{{ section.id }}" data-url="{{ product.url }}" {{ block.shopify_attributes }}>
                  {%- for option in product.options_with_values -%}
                      <fieldset class="js product-form__input custom-dispay-flex custom-swatch-{{ option.name }} custom-swatch-color {{ option.name }}">
                        <legend class="form__label">{{ option.name }}</legend>
                        {%- for value in option.values -%}
                        {%- assign variant_img_url = value | handle | append: '.' | append: file_extension | file_url  -%}

                          <input class="on_color_click" type="radio" id="{{ section.id }}-{{ option.position }}-{{ forloop.index0 }}"
                                name="{{ option.name }}" data-value="{{ value | downcase }}"
                                value="{{ value | escape }}"
                                form="{{ product_form_id }}"
                                {% if option.selected_value == value %}checked{% endif %}
                          >
                          <label color-name="{{ value }}" class="{{ value | handle }}" style="background: {{ value | escape }}; background-image: url('{{ variant_img_url }}') !important;" for="{{ section.id }}-{{ option.position }}-{{ forloop.index0 }}">
                          {% if option.name == 'Color' %}{% else %}  <span class="value_box">   {{ value }}</span>{% endif %}
                          </label>
                        {%- endfor -%}

                      </fieldset>
                  {%- endfor -%}
                  <script type="application/json">
                    {{ product.variants | json }}
                  </script>
                </variant-radios>
            <variant-selects class="no-js-hidden" data-section="{{ section.id }}" data-url="{{ product.url }}" {{ block.shopify_attributes }}>
                  {%- for option in product.options_with_values -%}
                    <div class="product-form__input product-form__input--dropdown {{ option.name }} size_custom_drop">
                      <label class="form__label" for="Option-{{ section.id }}-{{ forloop.index0 }}">
                        {{ option.name }}
                      </label>
                      <div class="select">
                        <select id="Option-{{ section.id }}-{{ forloop.index0 }}"
                          class="select__select chnagevalue_{{ option.name }}"
                          name="options[{{ option.name | escape }}]"
                          form="{{ product_form_id }}"
                        >
                          {%- for value in option.values -%}
                            <option data-value="{{ value | downcase }}" value="{{ value | escape }}" {% if option.selected_value == value %}selected="selected"{% endif %}>
                              {{ value }}
                            </option>
                          {%- endfor -%}
                        </select>
                        {% render 'icon-caret' %}
                      </div>
                    </div>
                  {%- endfor -%}

                  <script type="application/json">
                    {{ product.variants | json }}
                  </script>
                </variant-selects>
              {%- else -%}
                <variant-selects class="no-js-hidden" data-section="{{ section.id }}" data-url="{{ product.url }}" {{ block.shopify_attributes }}>
                  {%- for option in product.options_with_values -%}
                    <div class="product-form__input product-form__input--dropdown">
                      <label class="form__label" for="Option-{{ section.id }}-{{ forloop.index0 }}">
                        {{ option.name }}
                      </label>
                      <div class="select">
                        <select id="Option-{{ section.id }}-{{ forloop.index0 }}"
                          class="select__select"
                          name="options[{{ option.name | escape }}]"
                          form="{{ product_form_id }}"
                        >
                          {%- for value in option.values -%}
                            <option value="{{ value | escape }}" {% if option.selected_value == value %}selected="selected"{% endif %}>
                              {{ value }}
                            </option>
                          {%- endfor -%}
                        </select>
                        {% render 'icon-caret' %}
                      </div>
                    </div>
                  {%- endfor -%}

                  <script type="application/json">
                    {{ product.variants | json }}
                  </script>
                </variant-selects>
              {%- endif -%}
            {%- endunless -%}
