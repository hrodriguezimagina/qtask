<template></template>
<script>

export default {
  data() {
    return {
      crudId: this.$uid()
    }
  },
  computed: {
    crudData() {
      return {
        crudId: this.crudId,
        apiRoute: 'apiRoutes.qtask.tasks',
        permission: 'itask.categories',
        create: {
          title: this.$tr('itask.cms.newTask'),
        },
        read: {
          columns: [
            {name: 'id', label: this.$tr('isite.cms.form.id'), field: 'id', style: 'width: 50px'},
            {name: 'title', label: this.$tr('isite.cms.form.title'), field: 'title', align: 'rigth', isEditable: true},
            {name: 'description', label: this.$tr('isite.cms.form.description'), field: 'description', align: 'description', isEditable: true, style: 'width: 200px'},
            {name: 'startDate', label: this.$tr('isite.cms.form.startDate'), field: 'startDate', align: 'startDate', isEditable: true},
            {name: 'endDate', label: this.$tr('isite.cms.form.endDate'), field: 'endDate', align: 'endDate', isEditable: true},
            {name: 'statusId', label: this.$tr('isite.cms.form.status'), field: 'statusId', align: 'statusId', isEditable: true},
            {name: 'priorityId', label: this.$tr('itask.cms.form.priority'), field: 'priorityId', align: 'priorityId', isEditable: true},
            {name: 'estimatedTime', label: this.$tr('itask.cms.form.estimatedTime'), field: 'estimatedTime', align: 'estimatedTime', isEditable: true},
            {name: 'assignedToId', label: this.$tr('itask.cms.form.assigned'), field: 'assignedToId', align: 'assignedToId', isEditable: true},
            {name: 'categoryId', label: this.$tr('isite.cms.form.category'), field: 'categoryId', align: 'categoryId', isEditable: true},
            {
              name: 'created_at', label: this.$tr('isite.cms.form.createdAt'), field: 'createdAt', align: 'left',
              format: val => val ? this.$trd(val) : '-',
            },
            {
              name: 'updated_at', label: this.$tr('isite.cms.form.updatedAt'), field: 'updatedAt', align: 'left',
              format: val => val ? this.$trd(val) : '-',
            },
            {
              name: 'deleted_at', label: this.$tr('itask.cms.form.deletedAt'), field: 'deletedAt', align: 'left',
              format: val => val ? this.$trd(val) : '-',
            },
            {name: 'actions', label: this.$tr('isite.cms.form.actions'), align: 'left'},
          ],          
          filters: {}
        },
        update: {
          title: this.$tr('itask.cms.updateTask'),
        },
        delete: true,
        formLeft: {
          id: {value: ''},
          userId: {value: this.$store.state.quserAuth.userId},
          title: {
            value: '',
            type: 'input',
            props: {
              label: `${this.$tr('isite.cms.form.title')}*`,
              rules: [
                val => !!val || this.$tr('isite.cms.message.fieldRequired')
              ],
            },
          },
          description: {
            name : "description",
            value: '',
            type: 'html',
            props: {
              label: `${this.$tr('isite.cms.form.description')}*`,
              rules: [
                val => !!val || this.$tr('isite.cms.message.fieldRequired')
              ],
            }
          },
        },
        formRight: {          
          assignedToId: {
            value: [],
            type: 'select',
            props: {
              label: this.$tr('itask.cms.form.assigned'),
              //multiple: true,
              //useChips: true,
              useInput: true,
              rules: [
                val => !!val?.length || this.$tr('isite.cms.message.fieldRequired')
              ],
            },
            loadOptions: {
              apiRoute: 'apiRoutes.quser.users',              
              select: {
                label: 'email',
                id: item => `${item.id}`                
              }
            }
          },
          startDate: {
            value: '',            
            type: 'date',
            props: {
              label: this.$tr('isite.cms.form.startDate')
             }
          },        
          endDate: {
            value: '',            
            type: 'date',
            props: {
              label: this.$tr('isite.cms.form.endDate'),
            }
          },
          estimatedTime: {
            value: '',            
            type: 'input',
            props: {
              label: this.$tr('itask.cms.form.estimatedTime'),
            }
          },
          priorityId: {
            value: [],
            type: 'select',
            props: {
              label: this.$tr('itask.cms.form.priority'),             
              useInput: true,
              rules: [
                val => !!val?.length || this.$tr('isite.cms.message.fieldRequired')
              ],
            },
            loadOptions: {
              apiRoute: 'apiRoutes.qtask.priorities',
              select: {
                label: 'title',
                id: item => `${item.id}`
              }
            }
          },
          categoryId: {
            value: [],
            type: 'select',
            props: {
              label: this.$tr('isite.cms.form.category'),
              useInput: true,
              rules: [
                val => !!val?.length || this.$tr('isite.cms.message.fieldRequired')
              ],
            },
            loadOptions: {
              apiRoute: 'apiRoutes.qtask.categories',
              select: {
                label: 'title',
                id: item => `${item.id}`
              }
            }
          },
          statusId: {
            value: [],
            type: 'select',
            props: {
              label: this.$tr('isite.cms.form.status'),             
              useInput: true,
              rules: [
                val => !!val?.length || this.$tr('isite.cms.message.fieldRequired')
              ],
            },
            loadOptions: {
              apiRoute: 'apiRoutes.qtask.statuses',
              select: {
                label: 'title',
                id: item => `${item.id}`
              }
            }
          },
        }
      }
    },
    //Crud info
    crudInfo() {
      return this.$store.state.qcrudComponent.component[this.crudId] || {}
    }
  },
}
</script>
