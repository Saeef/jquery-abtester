# jquery-abtester

jQuery plugin for managing A/B Testing easily.

Manage the pattern that will be assigned to the user by using the Cookie.

## Installation

Include script *after* the jQuery library and jquery.cookie.js(https://github.com/carhartl/jquery-cookie) :

    <script src="/path/to/jquery-1.7.0.min.js"></script>
    <script src="/path/to/jquery.cookie.js"></script>
    <script src="/path/to/jquery.abtester.js"></script>
    
## Simple Usage

Anyway, please try to operate using the test.html.

For the elements under test, call the function abtester.
Set the duration of the test and cookieName.
Set the rate of appearance of each test pattern.
In addition, it is necessary to specify a pattern to be applied to the outside during the period when the period set
:

    $(function(){
        $('#abtest_target').abtester(
          {
            cookieName: 'uho',
            period: {
              start: new Date(2013, 0, 12, 18, 0, 0),
              end: new Date(2013, 0, 13, 21, 0, 0),
              outsidePattern: 'normal'
            },
            patterns: {
              normal: {
                probability: 10
              },
              a: {
                probability: 10
              },
              b: {
                probability: 10
              }
            }
          }
        );
      });
For the elements to be displayed for each pattern, and set the abtest class.
Specify the pattern using the attribute data-abtest :

    <div id="abtest_target">
      <div>
        will not removing when any pattern
      </div>
      <div class="abtest" data-abtest="normal">
        removing when not normal pattern
      </div>
      <div class="abtest" data-abtest="a" style="display:none">
        inserting only when A pattern
      </div>
      <div class="abtest" data-abtest="b" style="display:none">
        inserting only when B pattern
      </div>
      <div id="a_or_b" class="abtest" data-abtest="a, b" style="display:none">
        inserting only when A or B pattern
      </div>
    </div>
    <div id="unrelated_element" class="abtest" data-abtest="b">
      unrelated_element
    </div>

## Configuration

### Options for Cookie
Please edit the object of the function's arguments abtester.
it is depends on jquery-cookie plugin :

          {
            cookieName: 'uho',
            cookieOption: {
              path: '/',
              domain: 'example.com'
            }
          }
### Test Patterns
Please edit the object of the function's arguments abtester.

Need not necessarily be 100% of the total incidence of each pattern.
become a probability of 1/3 if you specify a = 10, b = 10, c = 10.

If for elements that occur in a pattern, and you want to process, such as animation, specify the function callback.

          {
            patterns: {
              normal: {
                probability: 10
              },
              a: {
                probability: 10
              },
              b: {
                probability: 10,
                callback:  function($self){
                  $(function(){
                    $self.find('#b_slide_down').slideDown('slow');
                  });
                }
              }
            }
          }

If you use the function callback, you will be considered in some cases it is necessary to disable the automatic display of the target element.
However, and should be false to attribute the data-auto-show of its elements. :

    <div id="abtest_target">
      <div>
        will not removing when any pattern
      </div>
      <div class="abtest" data-abtest="normal">
        removing when not normal pattern
      </div>
      <div class="abtest" data-abtest="a" style="display:none">
        inserting only when A pattern
      </div>
      <div id="b_slide_down" class="abtest" data-abtest="b" data-auto-show="false" style="display:none">
        inserting only when B pattern
      </div>
      <div id="a_or_b" class="abtest" data-abtest="a, b" style="display:none">
        inserting only when A or B pattern
      </div>
    </div>
    <div id="unrelated_element" class="abtest" data-abtest="b">
      unrelated_element
    </div>

