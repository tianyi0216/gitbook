# lec 06

Tensor dataset: torch.utils.data.TensorDataSet()



train,test = torch.utils.data.random\_split(ds, \[0.75, 0.25])



data loader: dl = torch.utils.data.DataLoader(train, batch\_size = 5, shuffle = True)
