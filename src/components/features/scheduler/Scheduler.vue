<template>
    <JqxScheduler ref="myScheduler"
                  :width="width" :height="600" :source="dataAdapter" :date="date" :view="'weekView'" :resources="resources"
                  :appointmentDataFields="appointmentDataFields" :views="views" :showLegend="true" :dayNameFormat="'abbr'" />
</template>

<script>
    import $ from "jquery";
    import JqxScheduler from '../../../jqwidgets-vue/vue_jqxscheduler.vue';

    import '../../../jqwidgets/styles/jqx.base.css';
    
    export default {
        name: 'sidemenu',
        components: {
          $,
          JqxScheduler
        },
        data: function () {
            return {
                width: 800,
                // eslint-disable-next-line no-undef
                date: new jqx.date(2016, 11, 23),
                appointmentDataFields:
                    {
                        from: 'start',
                        to: 'end',
                        id: 'id',
                        description: 'description',
                        location: 'place',
                        subject: 'subject',
                        resourceId: 'calendar'
                    },
                resources:
                    {
                        colorScheme: 'scheme05',
                        dataField: 'calendar',
                        orientation: 'horizontal',
                        // eslint-disable-next-line no-undef
                        source: new jqx.dataAdapter(this.source)
                    },
                views:
                    [
                        { type: 'dayView', showWeekends: false },
                        { type: 'weekView', showWeekends: false },
                        { type: 'monthView' }
                    ],
                // eslint-disable-next-line no-undef
                dataAdapter: new jqx.dataAdapter(this.source)
            }
        },
        beforeCreate: function () {
            const generateAppointments = function () {
                const appointments = new Array();
                const appointment1 = {
                    id: 'id1',
                    description: 'George brings projector for presentations.',
                    location: '',
                    subject: 'Quarterly Project Review Meeting',
                    start: new Date(2016, 10, 23, 9, 0, 0),
                    end: new Date(2016, 10, 23, 16, 0, 0)
                };
                const appointment2 = {
                    id: 'id2',
                    description: '',
                    location: '',
                    subject: 'IT Group Mtg.',
                    start: new Date(2016, 10, 24, 10, 0, 0),
                    end: new Date(2016, 10, 24, 15, 0, 0)
                };
                const appointment3 = {
                    id: 'id3',
                    description: '',
                    location: '',
                    subject: 'Course Social Media',
                    start: new Date(2016, 10, 27, 11, 0, 0),
                    end: new Date(2016, 10, 27, 13, 0, 0)
                };
                const appointment4 = {
                    id: 'id4',
                    description: '',
                    location: '',
                    subject: 'New Projects Planning',
                    start: new Date(2016, 10, 23, 0, 0, 0),
                    end: new Date(2016, 10, 25, 23, 59, 59)
                };
                const appointment5 = {
                    id: 'id5',
                    description: '',
                    location: '',
                    subject: 'Interview with James',
                    start: new Date(2016, 10, 25, 15, 0, 0),
                    end: new Date(2016, 10, 25, 17, 0, 0)
                };
                const appointment6 = {
                    id: 'id6',
                    description: '',
                    location: '',
                    subject: 'Interview with Nancy',
                    start: new Date(2016, 10, 26, 14, 0, 0),
                    end: new Date(2016, 10, 26, 16, 0, 0)
                };
 
                appointments.push(appointment1);
                appointments.push(appointment2);
                appointments.push(appointment3);
                appointments.push(appointment4);
                appointments.push(appointment5);
                appointments.push(appointment6);
 
                return appointments;
            };
 
            this.source =
                {
                    dataType: 'array',
                    dataFields: [
                        { name: 'id', type: 'string' },
                        { name: 'description', type: 'string' },
                        { name: 'location', type: 'string' },
                        { name: 'subject', type: 'string' },
                        { name: 'calendar', type: 'string' },
                        { name: 'start', type: 'date' },
                        { name: 'end', type: 'date' }
                    ],
                    id: 'id',
                    localData: generateAppointments()
                };        
        },
        mounted: function() {
              this.$refs.myScheduler.ensureAppointmentVisible('id1');
        }
    }
</script>